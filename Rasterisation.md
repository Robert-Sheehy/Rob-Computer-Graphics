# Rasterisation

Defn: Rasterisation is the process of deciding which pixels need to be "turn on" for a given primitive.  

Theory: Line Rasterisaion with Breshenhams Line Rasterisation Algorithm
Proctice:  A combination of Line and scan line algorithm for triangle rasterisation

## Where are we?

If we have just completed clipping, we can expect all primitives to be drawn will be in the Viewport, i.e. for the point (x,y) defining a primitive, $-1 \le x,y \le 1$

Rasterisation works on a screen which has its resolution, and all points will be defined using integer values.  How do we get from Clipping Space (Viewpor) to Rasterisation Space (Screen or Frame Buffer)

The conversion formula will be

Round $(\frac{(x+1)}2 (Res_x - 1))$  similarly for $y$  Round $(\frac{(y+1)}2 (Res_y - 1))$

These assume a screen resulution of $(Res_x, Res_y)$ and that the origin of the screen is bottom left. This is not always the case, sometimes it is top left.

Round $(\frac{(x+1)}2 (Res_x - 1))$  similarly for $y$  Round $(\frac{(1-y)}2 (Res_y - 1))$

##Line Rasterisation

The problem will always be phrased in terms of the end points of a line segment  $s = (s_x, s_y)$ and $e = (e_x, e_y)$

### Equation of the line Method

The equation of the line formula is $y - y_1 = m(x - x_1)$ where the slope $m = \frac{y_2 - y_1}{x_2 - x_1}$

The slope is calculated as $m = \frac{e_y - s_y}{e_x - s_x}$

So our equation of the line will be $y - s_y = m (x - s_x)$ which gives   $y = s_y + m (x - s_x)$  or $y = mx + s_y - ms_x$

To calculate any  $y_i$ for any $x_i$ we must evaluate $y_i = m * x_i +(s_y - ms_x)$. This requires a floating point multiplication and addition for each point, along with the added overhead of calculating the slope.


### Digital Differential Algorithm   (DDA)

### Breshenham Line Rasterisation

This algorithm breaks the whole process into a yes or no question,

<img width="268" height="248" alt="image" src="https://github.com/user-attachments/assets/08611f77-90bc-480f-a9a9-a770d8c65729" />

Should y increase or remain the same? The answer will depend on a decision parameter $p$, in particular if $p$ is positive or not.

As before, the problem will be defined in terms of the end points of a line segment  $s = (s_x, s_y)$ and $e = (e_x, e_y)$

The following are calculated:

$dx = e_x - s_x$

$dy = e_y - s_y$

$D = dy - dx \le 0$

$N = 2D  \le 0 $, where we call $N$ the negative adjustment.

$P = 2dy  /ge 0$, where we call $P$ the positive adjustment

$p_0 = 2dy - dx$  is the initial decision parameter, got by effectively saying go up with first is slope is greater than 0.5


<img width="518" height="355" alt="image" src="https://github.com/user-attachments/assets/5774410e-0415-4448-acef-bee1675ada68" />

Set $x_0 = s_x$ and $y_0 = s_y$

When determining the next set of values, we must use the following rules

$x_{i+1} = x_i +1$  i.e. increase $x$ by 1 everytime until you get to $x_i = e_x$

if $p \le 0$ then leave $y$ alone and add the positive adjustment to $p$.
otherwise $p > 0$ we increase $y$ and add the negative adjustment to $p$.



