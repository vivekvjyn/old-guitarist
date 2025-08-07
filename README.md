<h1>Old Guitarist</h2>

<p align="center"><img src="res/Screenshot.png" width="300"></p>

<br>

<p>
    Old guitarist is a physically modeled virtual guitar plugin.
</p>

- [x] Wave equation
- [ ] Stability condition
- [ ] Multiple Strings
- [x] IR Convolution
- [ ] Time-varying tension factor
- [ ] Hammer-ons
- [ ] Slides

## Physical Model

- $\gamma$: damping factor
- $\mu$: linear density
- $E$: Young's modulus
- $h$: Impulse response
- $I$: second moment of area ($\frac{\pi r^4}{4}$ for a cylinder)
- $l$: length
- $T$: tension
- $t$: time
- $x$: position

Wave equation for a guitar string is given as:

$$
\begin{align*}
\frac{\partial^2 y}{\partial x^2} - \frac{\mu}{T(t)} \frac{\partial^2 y}{\partial t^2} - \gamma \frac{\partial y}{\partial t} - EI \frac{\partial^4 y}{\partial x^4} = 0
\end{align*}
$$

### Conditions

$$
\begin{align*}
y(x, 0) =
\begin{cases} 
\frac{4x}{l} & \text{for } 0 \leq x < \frac{l}{4} \\
\frac{4 (l - x)}{3l} & \text{for } \frac{l}{4} \leq x \leq l
\end{cases}
\end{align*}
$$

$$
\begin{align*}
y(0, t) = y(l, t) = 0
\end{align*}
$$

### Finite Difference Method
Consider the expression given by

$$
\begin{align*}
f' = \lim_{{h \to 0}} \frac{{f(x + h) - f(x)}}{h}
\end{align*}
$$

&nbsp;&nbsp;&nbsp;&nbsp;In the context of the finite difference method, $h$ is a finite interval, and the difference quotient is used to approximate the derivative. Instead of taking the limit as $h$ approaches zero, a small but finite value of $h$ is chosen.

The wave equation is discretized to obtain the following form:

$$
\begin{align*}
\frac{y_{x+1}^{t} - 2y_{x}^{t} + y_{x-1}^{t}}{\Delta x^2} - \frac{\mu}{T(t)}\frac{y_{x}^{t+1} - 2y_{x}^{t} + y_{x}^{t-1}}{\Delta t^2}- \gamma \frac{y_{x}^{t+1} - y_{x}^{t-1}}{2 \Delta t} - EI \frac{y_{x-2}^{t} -4y_{x-1}^{t} + 6y_{x}^{t} - 4y_{x+1}^{t} + y_{x+2}^{t}}{\Delta x^4} = 0 
\end{align*}
$$

$$
\begin{align*}
Spatial \space resolution = \frac{1}{\Delta x}
\end{align*}
$$

$$
\begin{align*}
Temporal \space resolution = \frac{1}{\Delta t}
\end{align*}
$$

The stability analysis of finite difference schemes when applied to the numerical solution of partial differential equations is intricately tied to the Courant–Friedrichs–Lewy (CFL) condition, expressed as:

$$
\begin{align*}
C = \sqrt{\frac{\mu}{T}} \frac{\Delta x}{\Delta t} \leq C_{\text{max}}
\end{align*}
$$

$$
Spatial \space resolution \leq Temporal \space resolution \times \sqrt{\frac{\mu}{T}}
$$

&nbsp;&nbsp;&nbsp;&nbsp; $y^{t}$ is sampled for $x \in (0, l)$. The tone will vary with respect to x. Additionally, an impulse response of a guitar body is convoluted with $y$ to introduce body resonance.

$$
(y * h)(t) = \int_{-\infty}^{\infty} x(\tau) h(t - \tau) \, d\tau
$$

**Impulse response:** [Source](https://ccrma.stanford.edu/~jiffer8/420/project.html)
