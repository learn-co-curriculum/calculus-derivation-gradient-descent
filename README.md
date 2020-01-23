
#  Understanding the Gradient in Gradient Descent

### Introduction

As you know, we entered our discussion of derivatives to determine the size and direction of a step with which to move along a cost curve. We first used a derivative in a single variable function to see how the output of our cost curve changed with respect to a change in one of our regression line's variables. Then we learned about partial derivatives to see how a *three dimensional cost curve* responded to a change in the regression line.  

However, we have not yet explicitly showed how partial derivatives apply to gradient descent.

In this lesson we hope to explain how we can use partial derivatives to find the path that minimizes our cost function, and thus find our "best fit" regression line.

### What is the gradient?

Now gradient descent literally means that we are taking the shortest path to *descend* towards our minimum.  However, it is somewhat easier to understand gradient *ascent* than descent, and the two are quite related, so that's where we'll begin.  Gradient ascent, as you could guess, simply means that we want to **ascend** (move up) in the direction of the steepest slope from the point we are standing.

To determine the direction of steepest slope, we need to know how much we need to move in the $x$ direction and how much to move in the $y$ direction.  Thankfully, we have some notation that allows us to express direction very simply:  in mathematics (and physics) we use **vectors** to represent direction.  The vector $ (x, y) = (1, 2) $ means that we take one step in the $x$ direction and two steps in the $y$ direction (simple right?!).  Our job is to find the vector that will point in the direction of steepest slope! 

![](./Denali.jpg)

Note how this is a different task from what we have previously worked on for multivariable functions.   So far, we have used partial derivatives to calculate the **gain** from moving directly in either the $x$ direction or the $y$ direction.  

> Now, our task is not to calculate the gain from a move in either the $x$ or $y$ direction, but instead to **find some combination of change in both $x$ and $y$ that maximises our output**.  

So if you look at the path our climbers are taking in the picture above, *that* is the direction of gradient ascent.  If they tilt their path to the right or left, they will no longer be moving along the steepest upward path.

The **direction** of the greatest rate of increase of a function is called the gradient.  We denote the gradient with the nabla, which comes from the Greek word for harp, which is kind of what it looks like: $\nabla $.  So we can denote the gradient of a function, $f(x, y)$, with $\nabla f(x, y) $.

### Calculating the gradient

Now how do we find $\nabla f(x, y) $ (the direction for the greatest rate of increase)?  We use partial derivatives.  Here's why:

As we know, the partial derivative $\frac{\partial f}{\partial x}$ calculates the change in output from moving a little bit in the $x$ direction, and the partial derivative $\frac{\partial f}{\partial y}$ calculates the change in output from moving in the $y$ direction.  Because our goal is to make changes in $x, y$ that produces the greatest change in output, if $\frac{\partial f}{\partial y} > \frac{\partial f}{\partial x}$, we should make that move more in the $y$ direction than the $x$ direction, and vice versa.  That is, we want to get the biggest bang for our buck.  

![](./Denali.jpg)

Let's relate this again to the picture of our mountain climbers. Imagine the vertical edge on the left is our y-axis and the horizontal edge is on the bottom is our x-axis.  For the climber in the yellow jacket, imagine his step size is three feet. A step straight along the y-axis will move him further upwards than a step along the x-axis.  So in taking that step he should direct himself more towards the y-axis than the x-axis.  That will mean he's travelling up the steepest part of the mountain.

In fact, $\nabla f(x, y)$, is a **vector** which points in the direction of steepest ascent for a function (remember how we said before we wanted to find the vector that points us in the direction of steepest slope?  We just have!).  So, for example, if $\frac{\partial f}{\partial y}$ = 5 and $\frac{\partial f}{\partial x}$ = 1, this means we should walk 5 steps in the $y$ direction and 1 step in the $x$ direction in order to walk up the steepest part of the slope.  So, if $\nabla f(x, y)$ is the  vector that points in the direction of steepest slope, we have just discovered that the components of this vector are found by taking the partial derivatives of each variable, that is, $\nabla f(x, y) = (\frac{\partial f}{\partial x}, \frac{\partial f}{\partial y})$.  Now we have the tools to find the direction of steepest slope of ANY function.  

### Applying Gradient Descent 

Now that we have a better understanding of the gradient vector, let's apply our understanding to a multivariable function.  Here is a plot of a function:

$$f(x,y) = 2x + 3y $$

![](./3dx3y.png)

Imagine being at the bottom left of the graph at the point $x = 1$, $y = 1$.  What would be the direction of steepest ascent?  It seems, just sizing it up visually, that we should move both in the positive $y$ direction and the positive $x$ direction.  Looking more carefully, it seems we should move **more** in the $y$ direction than the $x$ direction.  Let's see what our technique of taking the partial derivative indicates.   

The gradient of the function $f(x,y)$, that is $ \nabla (2x + 3y $), is the vector: 

$(\frac{\partial f}{\partial x}(2x + 3y) = 2 $,  \frac{\partial f}{\partial y}(2x + 3y) = 3 )$.

So what this tells us is to move in the direction of greatest ascent for the function $f(x,y) = 2x + 3y $.  We move 2 steps to the right and 3 steps up!  So we would expect our path of greatest ascent to look like the following.

![](./gradient-plot.png)

![](./3dx3y.png)

So this path maps up well to what we see visually.  That is the idea behind gradient descent.  The gradient vector is the partial derivative with respect to each type of variable of a multivariable function, in this case $x$ and $y$.  And the importance of the gradient is that it points in the direction of steepest ascent.  The negative gradient, that is the negative of each of the partial derivatives, is the direction of steepest **descent**.  So our direction of gradient descent for the graph above is $x = -2$, $y = -3$.  And looking at the two graphs above, it seems that the steepest downward direction is just the opposite of the steepest upward direction.  Mathematically, we get this by simply multiplying $\nabla f(x, y)$ (and thus our partial derivatives) by -1.

### Summary

In this lesson, we saw how we can use gradient descent to find the **direction** of steepest descent.  We saw that the direction of steepest descent is some combination of a change in our variables to produce the greatest negative rate of change.  

We first saw how to calculate the gradient **vector** $\nabla $, the components of which are made up of the partial derivatives with respect to each variable.  Thus, $\nabla f(x, y) = (\frac{\partial f}{\partial x}, \frac{\partial f}{\partial y}) $.  This means that to take the path of steepest ascent, we should move in the direction of the gradient vector, i.e. ($ \frac{\partial f}{\partial x}, \frac{\partial f}{\partial y} $).  So, for example, when $ \frac{\partial f}{\partial y}f(x, y)  = 3 $ , and $ \frac{\partial f}{\partial x}f(x, y)  = 2$, travelling in the direction (2, 3) (2 steps in the x-direction, and 3 steps in the y-direction) will mean travelling in the direction of steepest ascent.  To determine the **size** of the **slope** of the path we're walking, we need to calculate the **magnitude** of the gradient vector.  In this case, the slope is $\sqrt(2^2 + 3^2)$ = $\sqrt(13)$ (don't worry too much about the details here).

To travel in the direction of steepest **descent** means to travel in the opposite direction of steepest **ascent**.  This simply means multiplying our gradient vector by -1.  Thus, $-\nabla f(x, y) = ( - \frac{\partial f}{\partial y}, - \frac{\partial f}{\partial x})$.  In this example, we have that $-\nabla f(x, y)  =  -(2, 3)  =  (-2, -3)$.
