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
$$\newcommand{\vect}[1]{\boldsymbol{#1}}
\newcommand{\cross}{\boldsymbol{\times}}
\vect{c} = \vect{a} \cdot \vect{b}
$$,
```cpp
Vector c = a ^ b;   // cross product of two vectors
```
expresses the vector cross product:
$$
\newcommand{\vect}[1]{\boldsymbol{#1}}
\newcommand{\cross}{\boldsymbol{\times}}
\vect{c} = \vect{a} \cross \vect{b}
$$,
and
```cpp
Vector c = R * a;   // rotation of a vector
```
expresses a rotation of the vector
$$
\newcommand{\vect}[1]{\boldsymbol{#1}}
\vect{a}
$$
by the rotation operator $$\mathit{R}$$ to give a vector
$$
\newcommand{\vect}[1]{\boldsymbol{#1}}
\vect{c}
$$.
<!-- A reference sheet for each class is made available in Appendix A and Appendix B. -->
A [Vector reference sheet]({% link /assets/Vector.pdf %}) as well as a
[Rotation reference sheet]({% link /assets/Rotation.pdf %}) are also available.



Rotations only require an axis and an angle of rotation&mdash;which is how they are stored&mdash;and may be specified in a number of convenient ways. We also provide methods for converting from the internal representation to the equivalent quaternion and rotation matrix representation. Quaternion algebra is summarized in Appendix C, which then provides a coordinate-free formula for the rotation of a vector.

It is also useful to describe rotations as a sequence of 3 standard rotations (Euler angles or yaw, pitch, and roll), and Appendix D shows that a rotation sequence about body axes is equivalent to the same rotation sequence applied in reverse order about fixed axes. There are a total of 12 rotation sequences that can be used to describe the orientation of a vector. In Appendix E we provide formulas1 for factoring an arbitrary rotation into each of these rotation sequences.
Rotations are commonly described with rotation matrices. Appendix F provides formulas and source code for converting between our descriptions of rotations, the quaternion representation, and the rotation matrix.

Quaternions are also very convenient and efficient for describing smooth rotations between 2 different orientations. Appendix G provides a derivation of the spherical linear interpolation (Slerp) formula for this purpose. We also provide a formula and coding for fast incremental Slerp.

Sometimes we need to relate 2 different orientations and find the rotation that will transform from one to the other. This is called the absolute orientation problem and Appendix H provides an exact solution to this problem.

The Rotation and Vector classes provide C++ support for all these operations. No libraries are required and there is nothing to build; one merely needs to include the header file to make use of the class. (The Rotation class includes the Vector class, so one only needs to include `Rotation.h` to also make use of the Vector class.)
