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
