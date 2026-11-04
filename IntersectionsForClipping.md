# Line Clipping

We are always going to have two points $s = (x_{0}, y_{0})$ and $e = (x_{1}, y_{1})$

We may need to slip this line segment against any of $y = 1, y = -1, x=-1$ or $x=1$

##Reminder  $y - y_{0} = m(x - x_{0})$ where $m = \frac{(y_{1} - y_{0})}{(x_{1} - X_{0})}$
Taking the easier ones first, if we wished to find the intersection of this line with the left or right edges of the viewport, then all we need to do is to substitute $x = -1$ or $x=1$ into the equation of the line to find the corresdponding $y$ coordinate for the respective intersections.

So  $y - y_{0} = m(x - x_{0})$  or  $y  =  y_{0} + m(x - x_{0})$ 

Left Intersection will be $(-1,  y_{0} + m(-1 - x_{0})$ 

Right Intersection will be $(1,  y_{0} + m(1 - x_{0})$ 

So for the top and the bottom edges we solve the equation of the line for $x$




