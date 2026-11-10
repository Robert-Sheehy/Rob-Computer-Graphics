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

