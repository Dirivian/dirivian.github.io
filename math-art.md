---
layout: page
permalink: /math-art/
---
I love making pretty plots. Here's a (disordered) collection of visualization I've made that I'm proud of enough to put on here.

#### **The rising thermal bubble**

This is a classic test case for fluid simulations. My code uses a well-balanced finite volume scheme to simulate Euler equations with gravity to get this visualization.

<p align="center">
<video src="/images/bubble.mp4" controls="controls" style="max-width: 300px;">
</video>
</p >

#### **The double periodic steady-state in the Kasimov Equation**

[This](https://journals.aps.org/prl/abstract/10.1103/PhysRevLett.110.104104) is one of the best papers I have read. The authors describe a beautifully simple model for shockwave chaos. The shock wave goes from constant to periodic to double periodic to chaotic as a single parameter changes. It inspired me to recreate the simulations using finite volume solvers in [Clawpack](https://www.clawpack.org/).

<p align="center">
<video src="/images/erit.mp4" controls="controls" style="max-width: 350px;"> 
</video> 
 </p >

The chaotic case can be seen [here[(https://www.youtube.com/watch?v=BFadoM801yg).

#### **Interactive visualization of the 3-card monte**

[Click here for an interactive story](https://dirivian.github.io/pages/monte/) using math to show that the 3-card monte is not really a game of skill.

[![Alternate Text](images/monte.jpg)](https://dirivian.github.io/pages/monte/)

#### **Fireflies in the night sky**

Fireflies sync up their flashes. Their flashes are periodic and the best way to see their behaviour is by plotting their blinks on a circle.
<p align="center">
<video src="/images/fireflies.mp4" height="4000" width="2000" controls="controls" style="max-width: 300px;">
</video>
</p >

See how to create simulations like these in my [Jupyter notebook](https://github.com/Dirivian/Atoms_and_Fireflies/blob/main/Fireflies.ipynb).

#### **A Jupyter Notebook on mathematical ecology**

[This notebook](https://github.com/Dirivian/Jupyter_notebooks/blob/master/Math_Ecology.ipynb) is a visual introduction to mathematical models used in ecology.

#### **A gif with no explanation**

![Alt Text](pages/animation.gif)

