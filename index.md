---
title: "Yop - A MATLAB Toolbox for Numerical Optimal Control based on CasADi"
keywords: homepage
sidebar: mydoc_sidebar
permalink: index.html
toc: false
---

Yop is a MATLAB Toolbox for numerical optimal control. It utilizes CasADi to interface to integrators and nonlinear optimization solvers, and thereof its name, Yop - Yet Another Optimal Control Problem Parser.

## Why yop?
Yop is made to simplify the step from mathematical formulation to code, giving the user time to focus on the optimal control problem. 

Take the classical Bryson-Denham optimal control problem with the following formulation:

$$\min_{a(t)} \frac{1}{2} \int_0^1 a(t)^2 dt$$

$$\dot{v}(t) = a(t) = u(t)$$

$$\dot{x}(t) = v(t)$$

$$v(0)=-v(1)=1$$

$$x(0)=x(1)=0$$

$$x(t) \leq l = \frac{1}{9}$$


In yop it is as simple as initializing the variables, formulating the ocp, calculating the solution and plotting the results.

```matlab
## Solution of the Bryson-Denham problem with yop.

# Initialize the variables
yopvar t0 tf t x1 x2 u

# Formulating the OCP
ocp = yop.ocp('Bryson-Denham Problem');
ocp.min( 1/2 * int(u^2) );
ocp.st( ...
    t0==0, tf==1, ...
    der(x1) == x2, ...
    der(x2) == u, ...
    x1(t0) == 0, ...
    x1(tf) == 0, ...
    x2(t0) == 1, ...
    x2(tf) == -1, ...
    x1 <= 1/9 ...
    );

# Calculate the solution
sol = ocp.solve('intervals', 15, 'degree', 2);

# Plot the results
figure(1);
subplot(311); hold on
sol.plot(t, x1, 'mag', 5);
subplot(312); hold on
sol.plot(t, x2);
subplot(313); hold on
sol.stairs(t, u);
```

#### Comparing yop to CasADi and PROPT 
To see how yop compares to some of its competition, check the following page.
[Comparinson between yop and casadi](benchmark)

### Getting started

<a target="_self" class="noCrossRef" href="{{ "install"}}"><button type="button" class="btn btn-default" aria-label="Left Align"><span class="glyphicon glyphicon-download-alt" aria-hidden="false"></span> Download Yop </button></a>

Download yop and then get started by reading our documentation or jumping directly into examples. 


* [Documentation](doc)
* [Examples](examples)

