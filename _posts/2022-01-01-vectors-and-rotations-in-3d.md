---
title: Vectors and Rotations in 3D
layout: post
keywords: vector, rotation, C++
katex: true
---

This document describes two C++ classes for performing vector algebra and vector rotations in 3D.
Each class is self-contained in a single header file (Vector.h and Rotation.h) so that a C++ programmer
only has to include the header file to make use of the code. Examples and reference sheets are provided to serve
as guidance in using the classes.

## Introduction



This document describes two C++ classes: a `Vector` class for performing vector algebra in 3-dimensional space (3D) and a `Rotation` class for performing rotations of vectors in 3D. These classes give the programmer the ability to use vectors and rotation operators in 3D as if they were native types in the C++ language. Thus, the code
```cpp
Vector c = a * b;   // dot product of two vectors
```
expresses the scalar dot product:
$$
\boldsymbol{c} = \boldsymbol{a} \cdot \boldsymbol{b}
$$,
```cpp
Vector c = a ^ b;   // cross product of two vectors
```
expresses the vector cross product:
$$
\boldsymbol{c} = \boldsymbol{a} \boldsymbol{\times} \boldsymbol{b}
$$,
and
```cpp
Vector c = R * a;   // rotation of a vector
```
expresses a rotation of the vector
$$
\boldsymbol{a}
$$
by the rotation operator $$\mathit{R}$$ to give a vector
$$
\boldsymbol{c}
$$.
<!-- A reference sheet for each class is made available in Appendix A and Appendix B. -->
A [Vector reference sheet]({% link /assets/vector_ref.pdf %}) as well as a
[Rotation reference sheet]({% link /assets/rotation_ref.pdf %}) are also available.



Rotations only require an axis and an angle of rotation&mdash;which is how they are stored&mdash;and may be specified in a number of convenient ways. We also provide methods for converting from the internal representation to the equivalent quaternion and rotation matrix representation. Quaternion algebra is summarized in [Appendix C]({% link /assets/rotation.pdf %}), which then provides a coordinate-free formula for the rotation of a vector.

It is also useful to describe rotations as a sequence of 3 standard rotations (Euler angles or yaw, pitch, and roll), and [Appendix D]({% link /assets/rotation.pdf %}) shows that a rotation sequence about body axes is equivalent to the same rotation sequence applied in reverse order about fixed axes. There are a total of 12 rotation sequences that can be used to describe the orientation of a vector. In [Appendix E]({% link /assets/rotation.pdf %}) we provide formulas1 for factoring an arbitrary rotation into each of these rotation sequences.
Rotations are commonly described with rotation matrices. [Appendix F]({% link /assets/rotation.pdf %}) provides formulas and source code for converting between our descriptions of rotations, the quaternion representation, and the rotation matrix.

Quaternions are also very convenient and efficient for describing smooth rotations between 2 different orientations. [Appendix G]({% link /assets/rotation.pdf %}) provides a derivation of the spherical linear interpolation (Slerp) formula for this purpose. We also provide a formula and coding for fast incremental Slerp.

Sometimes we need to relate 2 different orientations and find the rotation that will transform from one to the other. This is called the absolute orientation problem and [Appendix H]({% link /assets/rotation.pdf %}) provides an exact solution to this problem.

The Rotation and Vector classes provide C++ support for all these operations. No libraries are required and there is nothing to build; one merely needs to include the header file to make use of the class. (The Rotation class includes the Vector class, so one only needs to include [`Rotation.h`](https://github.com/rsaucier/Rotation) to also make use of the Vector class.)

## Using the Vector Class

The source code for the Vector class is completely self-contained in the header file
[`Vector.h`](https://github.com/rsaucier/Vector).
The program in Listing 1 provides some examples of how one might use the Vector class.
<figcaption class="caption">Listing 1. vtest.cpp</figcaption>
```cpp
// vtest.cpp: simple program to demonstrate basic usage of Vector class

#include "Vector.h"   // only need to include this header file
#include <iostream>
#include <cstdlib>
using namespace va;   // vector algebra namespace

int main( void ) {

   // let u be a unit vector that has equal components along all 3 axes
   Vector u = normalize( Vector( 1., 1., 1. ) );
   
   // output the vector
   std::cout << "u = " << u << std::endl;
   
   // show that the magnitude is 1
   std::cout << "magnitude = " << u.r() << std::endl;
   
   // output the polar angle in degrees
   std::cout << "polar angle (deg) = " << deg( u.theta() ) << std::endl;
   
   // output the azimuthal angle in degrees
   std::cout << "azimuthal angle (deg) = " << deg( u.phi() ) << std::endl;
   
   // output the direction cosines
   std::cout << "direction cosines = " << u.dircos( X ) << " " << u.dircos( Y ) << " " << u.dircos( Z ) << std::endl;
   
   // let ihat, jhat, khat be unit vectors along x-axis, y-axis, and z-axis, respectively
   Vector ihat( 1., 0., 0. ), jhat( 0., 1., 0. ), khat( 0., 0., 1. );
   
   // output the vectors
   std::cout << "ihat = " << ihat << std::endl;
   std::cout << "jhat = " << jhat << std::endl;
   std::cout << "khat = " << khat << std::endl;
   
   // rotate ihat, jhat, khat about u by 120 degrees
   ihat.rotate( u, rad( 120. ) );
   jhat.rotate( u, rad( 120. ) );
   khat.rotate( u, rad( 120. ) );
   
   // output the rotated vectors
   std::cout << "after 120 deg rotation about u:" << std::endl;
   std::cout << "ihat is now = " << ihat << std::endl;
   std::cout << "jhat is now = " << jhat << std::endl;
   std::cout << "khat is now = " << khat << std::endl;
   
   // define two vectors, a and b
   Vector a( 2., 1., -1. ), b( 3., -4., 1. );
   std::cout << "a = " << a << std::endl;
   std::cout << "b = " << b << std::endl;
   std::cout << "a + b = " << a + b << std::endl;
   std::cout << "a - b = " << a - b << std::endl;
   
   // compute and output the dot product
   double s = a * b;
   std::cout << "dot product, a * b = " << s << std::endl;
   
   // compute and output the cross product
   Vector c = a ^ b;
   std::cout << "cross product, a ^ b = " << c << std::endl;
   
   // output the angle (deg) between a and b
   std::cout << "angle between a and b (deg) = " << deg( angle( a, b ) ) << std::endl;
   
   // compute and output the projection of a along b
   std::cout << "proj( a, b ) = " << proj( a, b ) << std::endl;
   
   // rotate a and b 120 deg about u
   a.rotate( u, rad( 120. ) );
   b.rotate( u, rad( 120. ) );
   std::cout << "after rotating a and b 120 deg about u: " << a << std::endl;
   std::cout << "a is now = " << a << std::endl;
   std::cout << "b is now = " << b << std::endl;
   
   // output the angle (deg) between a and b
   std::cout << "angle between a and b (deg) is now = " << deg( angle( a, b ) ) << std::endl;
   
   // compute and output the dot product
   s = a * b;
   std::cout << "dot product, a * b is now = " << s << std::endl;
   
   // compute and output the cross product
   c = a ^ b;
   std::cout << "cross product, a ^ b is now = " << c << std::endl;
   
   // set a and b to their original values and compute the cross product
   a = Vector( 2., 1., -1. );
   b = Vector( 3., -4., 1. );
   c = a ^ b;
   std::cout << "original cross product, c = " << c << std::endl;
   
   // rotate c 120 deg about u and output
   c.rotate( u, rad( 120. ) );
   std::cout << "now rotate c 120 deg about u:" << std::endl;
   std::cout << "c is now = " << c << std::endl;

   return EXIT_SUCCESS;
}
```

Save this to a file `vtest.cpp` and compile it with the command
```
g++ -O2 -Wall -o vtest vtest.cpp -lm
```
Running it
```
./vtest
```
will print the following:

<figcaption class="caption">vtest output</figcaption>
```cpp
u = 0.57735 0.57735 0.57735
magnitude = 1
polar angle (deg) = 54.7356
azimuthal angle (deg) = 45
direction cosines = 0.57735 0.57735 0.57735
ihat = 1 0 0
jhat = 0 1 0
khat = 0 0 1
after 120 deg rotation about u:
ihat is now = 0 1 0
jhat is now = 0 0 1
khat is now = 1 0 0
a = 2 1 -1
b = 3 -4 1
a + b = 5 -3 0
a - b = -1 5 -2
dot product, a * b = 1
cross product, a ^ b = -3 -5 -11
angle between a and b (deg) = 85.4078
proj( a, b ) = 0.115385 -0.153846 0.0384615
after rotating a and b 120 deg about u: -1 2 1
a is now = -1 2 1
b is now = 1 3 -4
angle between a and b (deg) is now = 85.4078
dot product, a * b is now = 1
cross product, a ^ b is now = -11 -3 -5
original cross product, c = -3 -5 -11
now rotate c 120 deg about u:
c is now = -11 -3 -5
```

## Using the Rotation Class

Similarly, the source code for the Rotation class is completely self-contained in the header file
[`Rotation.h`](https://github.com/rsaucier/Rotation),
which is listed and described in [Appendix B]({% link /assets/rotation.pdf %}). The program in Listing 2 provides some basic examples of usage.

<figcaption class="caption">Listing 2. rtest.cpp</figcaption>

```cpp
// rtest.cpp

#include "Rotation.h"
#include <iostream>
#include <cstdlib>
#include <cmath>
#include <iomanip>
using namespace va;

int main( void ) {

   // declare two unit vectors, u and v
   Vector u = Vector( 1.5, 2.1, 3.2 ).unit(), v = Vector( 1.2, 3.5, -2.3 ).unit();
   std::cout << "u        = " << u << std::endl;
   std::cout << "v        = " << v << std::endl;
   
   // let R be the rotation specified by the vector cross product u ^ v
   Rotation R( u, v );
   
   // show that R * u equals v
   std::cout << "R * u    = " << R * u << std::endl;
   
   // interpolate a unit vector, w, halfway between u and v
   Vector w = slerp( u, v, 0.5 );
   std::cout << "Vector halfway between u and v = " << w << std::endl;
   
   // output angle between u and v
   std::cout << "angle between u and v (deg) = " << deg( angle( u, v ) ) << std::endl;
   
   // output angle between u and w
   std::cout << "angle between u and w (deg) = " << deg( angle( u, w ) ) << std::endl;
   
   // let Rinv be the inverse rotation
   Rotation Rinv = inverse( R );
   
   // show that Rinv * v equals u
   std::cout << "Rinv * v = " << Rinv * v << std::endl;
   
   Vector ihat( 1., 0., 0. ), jhat( 0., 1., 0. ), khat( 0., 0., 1. );
   R = Rotation( ihat, jhat, khat, jhat,khat, ihat );
   std::cout << "R = " << R << std::endl;
   
   sequence s = factor( R, ZYX );
   std::cout << "yaw (deg )   = " << deg( s.first ) << std::endl;
   std::cout << "pitch (deg ) = " << deg( s.second ) << std::endl;
   std::cout << "roll (deg )  = " << deg( s.third ) << std::endl;
   
   R = Rotation( s.first, s.second, s.third, ZYX );
   std::cout << "R = " << R << std::endl;
   
   s = factor( R, XYZ );
   std::cout << "pitch (deg ) = " << deg( s.first ) << std::endl;
   std::cout << "yaw (deg )   = " << deg( s.second ) << std::endl;
   std::cout << "roll (deg )  = " << deg( s.third ) << std::endl;
   
   std::streamsize ss = std::cout.precision();
   R = Rotation( s.first, s.second, s.third, XYZ );
   std::cout << "R = " << R << std::endl;
   
   rng::Random rng;
   R = Rotation( rng );
   std::cout << "R = " << R << std::endl;
   quaternion q = to_quaternion( R );
   std::cout << "the quaternion for this rotation is" << std::endl;
   std::cout << "q = " << q << std::endl;
   R = Rotation( q );
   std::cout << "R = " << R << std::endl;
   matrix A = to_matrix( R );
   std::cout << "the matrix for this rotation is" << std::endl;
   std::cout << std::setprecision(6) << std::fixed << std::showpos;
   std::cout << A << std::endl;
   
   std::cout << std::setprecision(ss) << std::noshowpos;
   R = Rotation( A );
   std::cout << "R = " << R << std::endl;
   
   u = normalize( Vector( 1., 1., 1. ) );
   double th = rad( 120. );
   R = Rotation( u, th );
   std::cout << R << std::endl;
   A = to_matrix( A );
   std::cout << A << std::endl;
   q = to_quaternion( R );
   std::cout << q << std::endl;
   
   return EXIT_SUCCESS;
}
```
Writing this to a file `rtest.cpp`, compiling and running it,
```
g++ -O2 -Wall -o rtest rtest.cpp -lm
./rtest
```
produces the following output:
<figcaption class="caption">rtest output</figcaption>
```cpp
u        = 0.364878 0.510829 0.778407
v        = 0.275444 0.803378 -0.527934
R * u    = 0.275444 0.803378 -0.527934
Vector halfway between u and v = 0.431716 0.886061 0.168873
angle between u and v (deg) = 84.264
angle between u and w (deg) = 42.132
Rinv * v = 0.364878 0.510829 0.778407
R = 0.57735 0.57735 0.57735	120
yaw (deg )   = -90
pitch (deg ) = -180
roll (deg )  = -90
R = 0.57735 0.57735 0.57735	120
pitch (deg ) = 45
yaw (deg )   = 90
roll (deg )  = 45
R = 0.57735 0.57735 0.57735	120
R = 0.338694 0.929155 0.148182	174.087
the quaternion for this rotation is
q = 0.0515815	0.338243 0.927918 0.147985
R = 0.338694 0.929155 0.148182	174.087
the matrix for this rotation is
-0.765862	+0.612457	+0.195837
+0.642990	+0.727384	+0.239741
+0.004383	+0.309530	-0.950880
R = 0.338694 0.929155 0.148182	174.086566
```

## Usage

To make use of the Vector class, simply include the [`Vector.h`](https://github.com/rsaucier/Vector)class file,
and to make use of both the Vector and Rotation classes,
simply include the [`Rotation.h`](https://github.com/rsaucier/Rotation) class file in your C++ program.
