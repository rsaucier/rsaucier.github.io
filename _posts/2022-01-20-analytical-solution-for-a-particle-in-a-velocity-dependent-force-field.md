---
author:
title: Analytical Solution for a Particle in a Velocity-Dependent Force Field
---

Introducing an integrating factor to solve a first-order linear differential equation, in the case of a  **vector** equation, also
serves as a generator for rotations.
In other words, the exponential $$\exp( J \omega t )$$, where $$J$$ is a matrix for the vector product, serves a dual role: as an integrating factor to analytically solve the differential equation, and at the same time 
consolidates the rotations to simple sine and cosine functions, which are readily integrable.
This technique[^1]
is explained and then applied to three velocity-dependent forces found in classical mechanics:
the Lorentz force, the Coriolis force, and the centrifugal force.

The coordinate-free formula for the counterclockwise rotation of a vector $$\boldsymbol{v}$$ about the unit vector $$\hat{\boldsymbol{n}}$$ through the angle $$\theta$$ is

$$
\boxed{R_{\hat{\boldsymbol{n}}} ( \theta ) \boldsymbol{v} = \boldsymbol{v} + \hat{\boldsymbol{n}} \boldsymbol{\times} \boldsymbol{v} \sin \theta + \hat{\boldsymbol{n}} \boldsymbol{\times} ( \hat{\boldsymbol{n}} \boldsymbol{\times} \boldsymbol{v} ) ( 1 - \cos \theta ) }. \tag{1}
$$

Let us transform this formula from a vector equation to a matrix equation.
Define the matrix operator $$J(\hat{\boldsymbol{n}})$$ as follows.

$$
\begin{aligned}[t]
J(\hat{\boldsymbol{n}} ) \boldsymbol{v} \equiv \hat{\boldsymbol{n}} \boldsymbol{\times} \boldsymbol{v} &= \begin{vmatrix} \hat{\boldsymbol{i}} & \hat{\boldsymbol{j}} & \hat{\boldsymbol{k}} \\ n_1 & n_2 & n_3 \\ v_1 & v_2 & v_3 \end{vmatrix} =
\hat{\boldsymbol{i}} ( n_2 v_3 - n_3 v_2 ) + \hat{\boldsymbol{j}} ( n_3 v_1 -  n_1 v_3 ) + \hat{\boldsymbol{k}} ( n_1 v_2 - n_2 v_1 ) \\
&= \begin{bmatrix} \phantom{-}0 & - n_3 & \phantom{-}n_2 \\ \phantom{-}n_3 & \phantom{-}0 & -n_1 \\ -n_2 & \phantom{-}n_1 & \phantom{-}0 \end{bmatrix} \begin{bmatrix} v_1 \\ v_2 \\ v_3 \end{bmatrix} ,
\end{aligned}
$$

where $$\hat{\boldsymbol{i}}$$, $$\hat{\boldsymbol{j}}$$, and $$\hat{\boldsymbol{k}}$$ are unit vectors along $$x$$, $$y$$, and $$z$$ axes, respectively, so that

$$
J(\hat{\boldsymbol{n}} ) \equiv \begin{bmatrix} \phantom{-}0 & - n_3 & \phantom{-}n_2 \\ \phantom{-}n_3 & \phantom{-}0 & -n_1 \\ -n_2 & \phantom{-}n_1 & \phantom{-}0 \end{bmatrix} .
$$

We see that
$$[ J(\hat{\boldsymbol{n}}) ]_{ij} = - \epsilon_{ijk} n_k$$, $$\det J = 0$$,  which implies $$J$$ has no inverse,
tr $$J = 0$$, and $$J^\dagger = - J$$.
Also, most importantly for our purposes,

$$
\hat{\boldsymbol{n}} \boldsymbol{\times} ( \hat{\boldsymbol{n}} \boldsymbol{\times} \boldsymbol{v} ) = J ( \hat{\boldsymbol{n}} ) ( \hat{\boldsymbol{n}} \boldsymbol{\times} \boldsymbol{v} ) = J(\hat{\boldsymbol{n}}) J(\hat{\boldsymbol{n}}) \boldsymbol{v} = J^2 ( \hat{\boldsymbol{n}} ) \boldsymbol{v} ,
$$

so that

$$
 J^3 ( \hat{\boldsymbol{n}} ) \boldsymbol{v} = \hat{\boldsymbol{n}} \boldsymbol{\times} [ \hat{\boldsymbol{n}} \boldsymbol{\times} ( \hat{\boldsymbol{n}} \boldsymbol{\times} \boldsymbol{v} ) ] = \hat{\boldsymbol{n}} \boldsymbol{\times} [ \hat{\boldsymbol{n}} ( \hat{\boldsymbol{n}} \cdot \boldsymbol{v} ) - \boldsymbol{v} ] = - \hat{\boldsymbol{n}} \boldsymbol{\times} \boldsymbol{v} = - J(\hat{\boldsymbol{n}}) \boldsymbol{v} .
$$

Hence,

$$
\boxed{J^3 = - J , \qquad J^4 = - J^2 , \qquad J^5 = - J^3 = J , \qquad J^6 = J^2 , \qquad \ldots} \tag{2}
$$

For completeness,

$$
J^2(\hat{\boldsymbol{n}} ) \equiv \begin{bmatrix}
- ( 1 - n_1^2 ) & n_1 n_2 & n_1 n_3 \\
n_1 n_2 & - ( 1 - n_2^2 ) & n_2 n_3 \\
n_1 n_3 & n_2 n_3 & - ( 1 - n_3^2 )
\end{bmatrix} ,
$$

although we will not need the explicit form of either $$J$$ or $$J^2$$.
Now, since the exponential of a matrix is defined by its power series, and making use of eq. (2), we have

$$
\begin{aligned}[t]
e^{J \theta} &= I + J \theta + \frac{(J\theta)^2}{2!} + \frac{(J\theta)^3}{3!} + \frac{(J\theta)^4}{4!} + \frac{(J\theta)^5}{5!} + \frac{(J\theta)^6}{6!} + \cdots \\
&= I + J \left ( \theta - \frac{\theta^3}{3!} + \frac{\theta^5}{5!} \mp \cdots \right ) + J^2 \left ( \frac{\theta^2}{2!} - \frac{\theta^4}{4!} + \frac{\theta^6}{6!} \mp \cdots \right ) \\
&= I + J \sin \theta + J^2 ( 1 - \cos \theta )
\end{aligned}
$$

so that $$J$$ is the **generator of rotations** and we can express the rotation operator in eq. (1) as

$$
\boxed{R_{\hat{\boldsymbol{n}}} ( \theta ) = e^{J(\hat{\boldsymbol{n}}) \theta} = I + J(\hat{\boldsymbol{n}}) \sin \theta + J^2(\hat{\boldsymbol{n}}) ( 1 - \cos \theta )} . \tag{3}
$$

&bull; **Lorentz Force**, $$\boldsymbol{F} = q ( \boldsymbol{E} + \boldsymbol{v} \boldsymbol{\times} \boldsymbol{B} )$$

The equation of motion for a charged particle of mass $$m$$ and charge $$q$$ in the presence of an electric field $$\boldsymbol{E}$$ and magnetic field $$\boldsymbol{B}$$, is

$$
m \frac{d\boldsymbol{v}}{dt} = q ( \boldsymbol{E} + \boldsymbol{v} \boldsymbol{\times} \boldsymbol{B} ) ,
$$

which we can rewrite as

$$
\frac{d\boldsymbol{v}}{dt} = \frac{q}{m} \boldsymbol{E} - \frac{qB}{m} \hat{\boldsymbol{b}} \boldsymbol{\times} \boldsymbol{v} = \frac{\omega}{B} \boldsymbol{E} - \omega \hat{\boldsymbol{b}} \boldsymbol{\times} \boldsymbol{v} =  \frac{\omega}{B} \boldsymbol{E} - \omega J ( \hat{\boldsymbol{b}} ) \boldsymbol{v}
$$

where $$\omega \equiv qB/m$$, $$\hat{\boldsymbol{b}} = \boldsymbol{B} / B$$, and $$J(\hat{\boldsymbol{b}}) \boldsymbol{v} = \hat{\boldsymbol{b}} \boldsymbol{\times} \boldsymbol{v}$$, or

$$
\frac{d \boldsymbol{v}}{d t} + \omega J(\hat{\boldsymbol{b}}) \boldsymbol{v} = \frac{\omega}{B} \boldsymbol{E} .
$$

An integrating factor for this first-order linear differential equation is $$e^{J ( \hat{\boldsymbol{b}} ) \omega t}$$, which gives

$$
\frac{d}{dt} \left ( e^{J ( \hat{\boldsymbol{b}} ) \omega t} \boldsymbol{v} \right ) = \dfrac{\omega}{B}  e^{J ( \hat{\boldsymbol{b}} ) \omega t} \boldsymbol{E} .
$$

Integrating,

$$
 e^{J ( \hat{\boldsymbol{b}} ) \omega t} \boldsymbol{v} (t) = \boldsymbol{v}_0 + \frac{\omega}{B}  \left ( \int_0^t e^{J ( \hat{\boldsymbol{b}} ) \omega \xi } d \xi \right ) \boldsymbol{E} ,
$$

and

$$
\boldsymbol{v} (t) =  e^{- J ( \hat{\boldsymbol{b}} ) \omega t} \boldsymbol{v}_0 + \frac{\omega}{B} \left ( \int_0^t e^{- J ( \hat{\boldsymbol{b}} ) \omega t} e^{J ( \hat{\boldsymbol{b}} ) \omega \xi} d \xi \right ) \boldsymbol{E} .
$$

Let $$\tau = t - \xi$$, $$d \tau = - d \xi$$, then the solution for the velocity is

$$
\boldsymbol{v} (t) =  e^{- J ( \hat{\boldsymbol{b}} ) \omega t} \boldsymbol{v}_0 + \frac{\omega}{B} \left ( \int_0^t e^{- J ( \hat{\boldsymbol{b}}) \omega \tau } d \tau \right ) \boldsymbol{E} .
$$

Integrating once more, the solution for the position is

$$
\boldsymbol{r}(t) = \boldsymbol{r}_0 + \left ( \int_0^t e^{- J ( \hat{\boldsymbol{b}} )\omega \tau } d \tau \right ) \boldsymbol{v}_0 + \frac{\omega}{B} \left ( \int_0^t \int_0^\tau e^{-  J ( \hat{\boldsymbol{b}} ) \omega \xi} d\xi d\tau \right ) \boldsymbol{E} .
$$

Making use of eq. (3), this can be written as

$$
\boldsymbol{r} (t) = \boldsymbol{r}_0 + \left ( \int_0^t R_{\hat{\boldsymbol{b}}} ( - \omega \tau ) \, d \tau \right ) \boldsymbol{v}_0 + \frac{\omega}{B} \left ( \int_0^t \int_0^\tau R_{\hat{\boldsymbol{b}}} ( - \omega \xi ) \, d\xi d\tau \right ) \boldsymbol{E} .
$$

Also from eq. (3),

$$
\begin{aligned}[t]
\int_0^t R_{\hat{\boldsymbol{b}}} (- \omega \tau) d\tau
&= t + \left ( \frac{\cos \omega t - 1}{\omega} \right ) J (\hat{\boldsymbol{b}}) + \left ( t - \frac{\sin \omega t}{\omega} \right ) J^2 (\hat{\boldsymbol{b}}) ,
\end{aligned}
$$

and

$$
\begin{aligned}[t]
\int_0^t \int_0^\tau R_{\hat{\boldsymbol{b}}} ( - \omega \xi) d\xi d\tau 
&= \frac{t^2}{2} + \left ( \frac{\sin \omega t}{\omega^2} - \frac{t}{\omega} \right ) J(\hat{\boldsymbol{b}}) + \left ( \frac{t^2}{2} + \frac{\cos \omega t - 1}{\omega^2} \right ) J^2(\hat{\boldsymbol{b}}) ,
\end{aligned}
$$

so that, we find (see the full [paper](https://rsaucier.github.io/assets/vel_dep_forces.pdf) for details)

$$
 \boxed{\begin{aligned}[t]
\boldsymbol{r}(t) &= \boldsymbol{r}_0 + \boldsymbol{v}_0 t + \frac{\omega t^2}{2 B} \hat{\boldsymbol{b}} ( \hat{\boldsymbol{b}} \cdot \boldsymbol{E} ) +
 \left ( \frac{1 - \cos \omega t}{\omega}\right ) \left ( -\hat{\boldsymbol{b}} \boldsymbol{\times} \boldsymbol{v}_0 - \frac{1}{B}  \hat{\boldsymbol{b}} \boldsymbol{\times} ( \hat{\boldsymbol{b}} \boldsymbol{\times} \boldsymbol{E} )  \right ) \\
 & \hspace{1em} + \left ( t - \frac{\sin \omega t}{\omega} \right ) \left (  \hat{\boldsymbol{b}} \boldsymbol{\times} ( \hat{\boldsymbol{b}} \boldsymbol{\times} \boldsymbol{v}_0 )  - \frac{1}{B} ( \hat{\boldsymbol{b}} \boldsymbol{\times} \boldsymbol{E} ) \right ) . \tag{4}
\end{aligned}}
$$

&bull; **Coriolis Force**, $$\boldsymbol{F} = m \boldsymbol{g} - 2 m \, \boldsymbol{\Omega} \boldsymbol{\times} \boldsymbol{v}$$

The equation of motion for a particle of mass $$m$$ in the presence of gravity while in a non-inertial frame of reference with rotational velocity $$\boldsymbol{\Omega}$$ is

$$
m \frac{d \boldsymbol{v}}{dt} = m \boldsymbol{g} - 2 m \, \boldsymbol{\Omega} \boldsymbol{\times} \boldsymbol{v} ,
$$

which we can rewrite as

$$
\frac{d \boldsymbol{v}}{dt} + 2 \Omega \, J ( \hat{\boldsymbol{\omega}} ) \boldsymbol{v}  = \boldsymbol{g} ,
$$

where $$\hat{\boldsymbol{\omega}} = \boldsymbol{\Omega} / \Omega$$ and $$J(\hat{\boldsymbol{\omega}}) \boldsymbol{v} = \boldsymbol{\omega} \boldsymbol{\times} \boldsymbol{v}$$.
An integrating factor is $$e^{2 J(\hat{\boldsymbol{\omega}})\Omega t }$$, which gives

$$
\frac{d}{dt} \left ( e^{2 J(\hat{\boldsymbol{\omega}}) \Omega t } \boldsymbol{v} \right ) = e^{2 J(\hat{\boldsymbol{\omega}}) \Omega t } \boldsymbol{g}
$$

and integrates to

$$
 e^{2 J(\hat{\boldsymbol{\omega}})\Omega t } \boldsymbol{v}(t) = \boldsymbol{v}_0 + \left ( \int_0^t e^{2 J(\hat{\boldsymbol{b}}) \Omega \xi } d \xi \right ) \boldsymbol{g}
$$

or

$$
\boldsymbol{v}(t) = e^{-2 J(\hat{\boldsymbol{\omega}}) \Omega t} \boldsymbol{v}_0 +  \left ( \int_0^t e^{-2 J(\hat{\boldsymbol{\omega}}) \Omega t } e^{2  J(\hat{\boldsymbol{b}}) \Omega \xi} d \xi \right ) \boldsymbol{g} .
$$

Changing variables with $$\tau = t - \xi$$, $$d \tau = - d \xi$$, we have

$$
\boldsymbol{v}(t) = e^{-2 J(\hat{\boldsymbol{\omega}}) \Omega t} \boldsymbol{v}_0 +  \left ( \int_0^t e^{-2 J(\hat{\boldsymbol{\omega}}) \Omega \tau} d \tau \right ) \boldsymbol{g} ,
$$

and the solution for the position vector is

$$
\begin{aligned}[t]
\boldsymbol{r}(t) &= \boldsymbol{r}_0 + \left ( \int_0^t e^{- 2J ( \hat{\boldsymbol{\omega}} ) \Omega \tau } d \tau \right ) \boldsymbol{v}_0 + \left ( \int_0^t \int_0^\tau e^{- 2 J ( \hat{\boldsymbol{\omega}} ) \Omega \xi} d\xi d\tau \right ) \boldsymbol{g} \\
&= \boldsymbol{r}_0 + \left ( \int_0^t R_{\hat{\boldsymbol{\omega}}} ( - 2 \Omega \tau ) \, d \tau \right ) \boldsymbol{v}_0 + \left ( \int_0^t \int_0^\tau R_{\hat{\boldsymbol{\omega}}} ( - 2 \Omega \xi ) \, d\xi d\tau \right ) \boldsymbol{g} .
\end{aligned}
$$

Putting everything together, we get

$$
\boxed{\begin{aligned}[t]
\boldsymbol{r}(t) &= \boldsymbol{r}_0 + \boldsymbol{v}_0 t + \frac{1}{2} \boldsymbol{g} t^2 + \frac{1}{2} \hat{\boldsymbol{\omega}} \boldsymbol{\times} ( \hat{\boldsymbol{\omega}} \boldsymbol{\times} \boldsymbol{g} ) t^2 \\
& \hspace{1em} - \left ( \frac{1 - \cos 2 \Omega t}{2 \Omega} \right ) \left ( \hat{\boldsymbol{\omega}} \boldsymbol{\times} \boldsymbol{v}_0 + \frac{1}{2 \Omega} \hat{\boldsymbol{\omega}} \boldsymbol{\times} ( \hat{\boldsymbol{\omega}} \boldsymbol{\times} \boldsymbol{g} ) \right ) \\
& \hspace{1em} - \left ( t - \frac{\sin 2 \Omega t}{2 \Omega} \right ) \left ( \frac{1}{2 \Omega} \hat{\boldsymbol{\omega}} \boldsymbol{\times} \boldsymbol{g} - \hat{\boldsymbol{\omega}} \boldsymbol{\times} ( \hat{\boldsymbol{\omega}} \boldsymbol{\times} \boldsymbol{v}_0 ) \right )
\end{aligned}} \tag{5}
$$

&bull; **Both Coriolis and Centrifugal Force**, $$\boldsymbol{F} = m \boldsymbol{g} - 2 m \, \boldsymbol{\Omega} \boldsymbol{\times} \boldsymbol{v} - m \, \boldsymbol{\Omega} \boldsymbol{\times} ( \boldsymbol{\Omega} \boldsymbol{\times} \boldsymbol{r} )$$

The rate of change of any vector in an inertial frame of reference (*fixed frame*) is equal to the rate of change of the vector in the *rotating frame* plus the vector product of the angular velocity, $$\boldsymbol{\Omega}$$,
with the given vector.[^2]

Thus we have the operator equation:

$$
\left ( \frac{d}{dt} \right )_\text{fixed} = \left ( \frac{d}{dt} \right )_\text{rotating}+ \boldsymbol{\Omega} \, \boldsymbol{\times}
$$

Applied to the position vector, we have

$$
\begin{aligned}[t]
\dot{\boldsymbol{r}}_\text{fixed} &= \left [  \left ( \frac{d}{dt} \right )_\text{rotating} + \boldsymbol{\Omega} \, \boldsymbol{\times} \right ] \boldsymbol{r} = \dot{\boldsymbol{r}} + \boldsymbol{\Omega} \boldsymbol{\times} \boldsymbol{r} \\
\ddot{\boldsymbol{r}}_\text{fixed} &= \left [  \left ( \frac{d}{dt} \right )_\text{rotating} + \boldsymbol{\Omega} \, \boldsymbol{\times} \right ] ( \dot{\boldsymbol{r}} + \boldsymbol{\Omega} \boldsymbol{\times} \boldsymbol{r} ) \\
&= \left [  \left ( \frac{d}{dt} \right )_\text{rotating} + \boldsymbol{\Omega} \boldsymbol{\times} \right ] \dot{\boldsymbol{r}} + \left [  \left ( \frac{d}{dt} \right )_\text{rotating} + \boldsymbol{\Omega} \, \boldsymbol{\times} \right ] ( \boldsymbol{\Omega} \, \boldsymbol{\times} \boldsymbol{r} ) \\
&= \ddot{\boldsymbol{r}} + \boldsymbol{\Omega} \boldsymbol{\times} \dot{\boldsymbol{r}} + \dot{\boldsymbol{\Omega}} \boldsymbol{\times} \boldsymbol{r} + \boldsymbol{\Omega} \boldsymbol{\times} \dot{\boldsymbol{r}} + \boldsymbol{\Omega} \boldsymbol{\times} ( \boldsymbol{\Omega} \boldsymbol{\times} \boldsymbol{r} ) \\
&= \ddot{\boldsymbol{r}} + \underbrace{2 \boldsymbol{\Omega} \boldsymbol{\times} \dot{\boldsymbol{r}} + \dot{\boldsymbol{\Omega}} \boldsymbol{\times} \boldsymbol{r}}_{\text{Coriolis force}} + \underbrace{\boldsymbol{\Omega} \boldsymbol{\times} ( \boldsymbol{\Omega} \boldsymbol{\times} \boldsymbol{r} )}_{\text{Centrifugal force}}
\end{aligned}
$$

The total force is

$$
\boldsymbol{F} = m \boldsymbol{a}_\text{fixed} = m \boldsymbol{a}_\text{rotating} + 2 m \boldsymbol{\Omega} \boldsymbol{\times} \boldsymbol{v}_\text{rotating} + m \dot{\boldsymbol{\Omega}} \boldsymbol{\times} \boldsymbol{r} + m \boldsymbol{\Omega} \boldsymbol{\times} ( \boldsymbol{\Omega} \boldsymbol{\times} \boldsymbol{r} )
$$

For an observer in the rotating frame, the effective force is

$$
\boldsymbol{F}_{\text{eff}} \equiv m \boldsymbol{a}_\text{rotating} = m \boldsymbol{g} - 2 m \boldsymbol{\Omega} \boldsymbol{\times} \dot{\boldsymbol{r}} - m \dot{\boldsymbol{\Omega}} \boldsymbol{\times} \boldsymbol{r} - m \boldsymbol{\Omega} \boldsymbol{\times} ( \boldsymbol{\Omega} \boldsymbol{\times} \boldsymbol{r} ) 
$$

Thus, the equation of motion in the *rotating frame* is

$$
\begin{aligned}[t]
\ddot{\boldsymbol{r}} + 2 \boldsymbol{\Omega} \boldsymbol{\times} \dot{\boldsymbol{r}} + \dot{\boldsymbol{\Omega}} \boldsymbol{\times} \boldsymbol{r} +  \boldsymbol{\Omega} \boldsymbol{\times} ( \boldsymbol{\Omega} \boldsymbol{\times} \boldsymbol{r} ) &= \boldsymbol{g} \\
\ddot{\boldsymbol{r}} + 2 \Omega J(\hat{\boldsymbol{\omega}}) \dot{\boldsymbol{r}} +  [ \dot{\Omega} J(\hat{\boldsymbol{\omega}}) + \Omega^2 J^2(\hat{\boldsymbol{\omega}} )  ] \boldsymbol{r} &= \boldsymbol{g}
\end{aligned}
$$

We rewrite this as[^3]

$$
\ddot{\boldsymbol{r}} + 2 A (t) \dot{\boldsymbol{r}} + B(t) \boldsymbol{r} = \boldsymbol{g}
$$

where $$A(t)$$ and $$B(t)$$ are the matrices $$A(t) \equiv \Omega J(\hat{\boldsymbol{\omega}})$$ and $$B(t) \equiv \dot{\Omega} J(\hat{\boldsymbol{\omega}}) + \Omega^2 J^2(\hat{\boldsymbol{\omega}} )$$.
Let $$\boldsymbol{r} = V(t) \, \boldsymbol{y}$$, then

$$
\begin{aligned}[t]
\dot{\boldsymbol{r}} &= \dot{V} \boldsymbol{y} + V \dot{\boldsymbol{y}} \\
\ddot{\boldsymbol{r}} &= \ddot{V} \boldsymbol{y} + 2 \dot{V} \dot{\boldsymbol{y}} + V \ddot{\boldsymbol{y}} ,
\end{aligned}
$$

which transforms eq. (6) into

$$
\begin{aligned}[t]
\ddot{V} \boldsymbol{y} + 2 \dot{V} \dot{\boldsymbol{y}} + V \ddot{\boldsymbol{y}} + 2A ( \dot{V} \boldsymbol{y} + V \dot{\boldsymbol{y}} ) + B V \boldsymbol{y} &= \boldsymbol{g} \\
V \ddot{\boldsymbol{y}}  + 2 ( \dot{V} + A V ) \dot{\boldsymbol{y}} + ( \ddot{V} + 2 A \dot{V} + B V ) \boldsymbol{y} &= \boldsymbol{g}
\end{aligned}
$$

And now we choose $$V$$ to eliminate the $$\dot{\boldsymbol{y}}$$ term:

$$
\dot{V} + A V = 0 \quad \implies \quad \dot{V} = - A V \quad \implies \quad V = e^{-A t} .
$$

Also

$$
\dot{V} = - A V \quad \implies \quad \ddot{V} = - \dot{A} V - A \dot{V} = - \dot{A} V + A^2 V ,
$$

so that eq. (7) becomes

$$
\begin{aligned}[t]
V \ddot{\boldsymbol{y}} + ( - \dot{A} V + A^2 V - 2 A^2 V+ BV ) \boldsymbol{y} &= \boldsymbol{g} \\
V \ddot{\boldsymbol{y}} + ( B - A^2 - \dot{A} ) V \boldsymbol{y} &= \boldsymbol{g}
\end{aligned}
$$

Now, using the expressions for $$A$$ and $$B$$, we find that the coefficient of $$\boldsymbol{y}$$ also vanishes:

$$
\begin{aligned}[t]
B - A^2 - \dot{A} &= \dot{\Omega} J(\hat{\boldsymbol{\omega}}) + \Omega^2 J^2(\hat{\boldsymbol{\omega}}) - \Omega^2 J^2(\hat{\boldsymbol{\omega}})  - \dot{\Omega} J(\hat{\boldsymbol{\omega}}) = 0
\end{aligned}
$$

Thus, eq. (8) reduces to simply

$$
V \ddot{\boldsymbol{y}} = \boldsymbol{g}
$$

and therefore we have

$$
\ddot{\boldsymbol{y}} = V^{-1} \boldsymbol{g} = e^{At} \boldsymbol{g} = e^{J(\hat{\boldsymbol{\omega}}) \Omega t} \boldsymbol{g} = [ I + J(\hat{\boldsymbol{\omega}}) \sin \Omega t + J^2(\hat{\boldsymbol{\omega}}) ( 1 - \cos \Omega t ) ] \boldsymbol{g}
$$

For convenience, let's write $$J$$ for $$J( \hat{\boldsymbol{\omega}} )$$. Starting with

$$
\ddot{\boldsymbol{y}} =  [ I + \sin \Omega t J + ( 1 - \cos \Omega t ) J^2 ] \boldsymbol{g}
$$

and integrating over time twice, we get

$$
\boldsymbol{y}(t) = \boldsymbol{y}(0) + \dot{\boldsymbol{y}} (0) t + \frac{1}{2} \boldsymbol{g} t^2 + \frac{\Omega t - \sin \Omega t}{\Omega^2} J \boldsymbol{g} + \frac{\Omega^2 \frac{1}{2} t^2 + \cos \Omega t - 1}{\Omega^2} J^2 \boldsymbol{g}
$$

Now, $$\boldsymbol{r}_0 = \boldsymbol{y}(0)$$ and $$\boldsymbol{v}_0 \equiv \dot{r}_0 = \dot{\boldsymbol{y}}(0) - \Omega J \boldsymbol{y}(0)$$, so that we can make the replacements

$$
\begin{aligned}[t]
\boldsymbol{y}(0) &\implies \boldsymbol{r}_0 \\
\dot{\boldsymbol{y}}(0) &\implies \boldsymbol{v}_0 + \Omega J \boldsymbol{r}_0
\end{aligned}
$$

Also, $$\boldsymbol{r}(t)$$ and $$\boldsymbol{y}(t)$$ are related by the transformation $$\boldsymbol{r}(t) = e^{-J \Omega t } \boldsymbol{y}(t)$$.
Thus, we have

$$
\begin{aligned}[t]
\boldsymbol{r}(t) &= e^{-J \Omega t} \left [ \boldsymbol{r}_0 + \boldsymbol{v}_0 t + \Omega J \boldsymbol{r}_0 t + \frac{1}{2} \boldsymbol{g}t^2 + \frac{\Omega t - \sin \Omega t}{\Omega^2} J \boldsymbol{g} + \frac{\frac{1}{2} \Omega^2t^2 + \cos \Omega t - 1}{\Omega^2} J^2 \boldsymbol{g} \right ] \\
&= e^{-J \Omega t} \left \{ \boldsymbol{r}_0 + \boldsymbol{v}_0 t + \frac{1}{2} \boldsymbol{g} t^2 - \frac{1}{\Omega^2} \underbrace{\left [ I + \sin \Omega t J + ( 1 - \cos \Omega t ) J^2 \right ]}_{e^{J \Omega t}} \boldsymbol{g} + \Omega J \boldsymbol{r}_0 t + \frac{1}{\Omega^2} \left [ I + \Omega t J + \frac{1}{2} \Omega^2 t^2 J^2 \right ] \boldsymbol{g} \right \}
\end{aligned}
$$

After a bit of algebra (see [paper](https://rsaucier.github.io/assets/vel_dep_forces.pdf) for details), and using $$J^3 = -J$$ and $$J^4 = -J^2$$, the final formula is

$$
\boxed{
\begin{aligned}[t]
\boldsymbol{r}(t) = \hspace{0.25em} &\boldsymbol{r}_0 + \boldsymbol{v}_0 t + \frac{1}{2} \boldsymbol{g} t^2 + \hat{\boldsymbol{\omega}} \boldsymbol{\times} [ \hat{\boldsymbol{\omega}} \boldsymbol{\times} ( \boldsymbol{r}_0^* + \boldsymbol{v}_0 t + \frac{1}{2} \boldsymbol{g} t^2 ) ] 
-\sin \Omega t ( \hat{\boldsymbol{\omega}} \boldsymbol{\times} \boldsymbol{r}_0^* ) - \cos \Omega t [ \hat{\boldsymbol{\omega}} \boldsymbol{\times} ( \hat{\boldsymbol{\omega}} \boldsymbol{\times} \boldsymbol{r}_0^* ) ] \\
&- \Omega t \sin \Omega t \left [ \hat{\boldsymbol{\omega}} \boldsymbol{\times} ( \hat{\boldsymbol{\omega}} \boldsymbol{\times} \boldsymbol{r}_0^* ) + \frac{1}{\Omega} ( \hat{\boldsymbol{\omega}} \boldsymbol{\times} \boldsymbol{v}_0 ) \right ] 
 + \Omega t \cos \Omega t \left [ ( \hat{\boldsymbol{\omega}} \boldsymbol{\times} \boldsymbol{r}_0^* ) - \frac{1}{\Omega} \hat{\boldsymbol{\omega}} \boldsymbol{\times} ( \hat{\boldsymbol{\omega}} \boldsymbol{\times} \boldsymbol{v}_0 ) \right ]
 \end{aligned}}
$$

[^1]: J. M. Y&aacute;&ntilde;ez, G. Guti&eacute;rrez, F. Gonz&aacute;lez-Cataldo, and D. Laroze, <q>An exact solution for a particle in a velocity-dependent force field,</q> [Am. J. Phys.](https://aapt.scitation.org/doi/10.1119/10.0005992) **89**(12), 1103-1112 (2021).

[^2]: J. B. Marion, *Classical Dynamics of Particles and Systems* (Academic Press, New York, 1965).

[^3]: L. Y. Bahar, <q>Generalized Gantmacher formulas through functions of matrices,</q> [Am. J. Phys.](https://aapt.scitation.org/doi/10.1119/1.16621) **59**(12), 1103--1111 (1991).
