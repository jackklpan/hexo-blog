---
title: Imgae alignment
tags: []
date: 2015-02-07 15:33:00
---

# Newton’s method: 
Find the f(x) = 0\. 
For an initialized point, calculate the tangent line. And set the point that is intersection of x-axis and tangent line as next x. 
As the animated picture from wiki: 
![](http://upload.wikimedia.org/wikipedia/commons/e/e0/NewtonIteration_Ani.gif) 
So write in math: 
\( x_{n+1} = x_n - \frac{f(x_n)}{f^\prime(x_n)} \) 

# Lucas-Kanade:
When in image alignment that **only translation**: 
\( E(u, v) = \sum_{x,y}{(I(x+u, y+v) - T(x, y))}^2 \) 
Do Taylor's expand in I(x+y, y+v): 
\( E(u, v) = \sum_{x,y}{(I(x, y) - T(x, y) + uI_x + + vI_y)}^2 \) 
And differentiate to find the extremal point: 
\( 0 = \frac{\partial E}{\partial u} = \sum_{x,y}{2I_x(I(x,y)-T(x,y)+uI_x+vI_y)} \) 
\( 0 = \frac{\partial E}{\partial v} = \sum_{x,y}{2I_y(I(x,y)-T(x,y)+uI_x+vI_y)} \) 
Reformat as matrix: 
\( \begin{bmatrix} \sum_{x,y}{I_x^2} & \sum_{x,y}{I_xI_y} \\ \sum_{x,y}{I_xI_y} & \sum_{x,y}{I_y^2} \end{bmatrix}  \begin{bmatrix} u \\ v \end{bmatrix} = \begin{bmatrix} \sum_{x,y}{I_x(T(x,y)-I(x,y))} \\ \sum_{x,y}{I_y(T(x,y)-I(x,y))} \end{bmatrix}  \) 
One thing to note: 
Although in the math is plus u and v. 
But if we write in transformation matrix, it is minus u and v. 
**Because I(x+u, y+v) means original x, y becomes the x-y, y-v in a transformed image. ** 

circular convolution 
 1\. why don't just use translation matrix to fit 
2\. d/dx d/dy use which kernel is better 