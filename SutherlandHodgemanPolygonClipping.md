# Polygon Clipping

Defn: A Polygon is a sequence of 2D vertices $v_{0}, v_{1}, \dots, v_{n-1}$ where each edge goes from $v_{i}$ to $v_{i+1}$  and there is a final edge from $v_{n-1}$ to $v_{0}$
## Sutherland Hodgeman

In this algorithm, a "Divide and Conquer" approach is taken to clip a polygon against a viewport, which consists of 4 edges, Top $y=1$, Bottom $y=-1$, Left $x = -1$ and Right $x=1$

To this it clips the polygon against a single edge, and passes the result on the the next stage, which deals with the next edge of the viewport.

Graphically, it might look something like this...

<img width="699" height="469" alt="image" src="https://github.com/user-attachments/assets/c528367c-1f2b-4396-abdc-de12b0f49e8e" />
 Against top edge (green)

 <img width="700" height="439" alt="image" src="https://github.com/user-attachments/assets/005ead75-1cce-4159-adca-ab0ff13994b6" />

In practice, the process of clipping against an given edge, invloves taking each line segment of the polygon an processing that line segment against the edge...

For a given line segment $v_{i}$ to $v_{i+1}$ clipped against a viewport edge

|Input Description | Output |
| :--- | :--- |
| In to In  | $v_{i}$ |
| In to Out | $v_{i}, v_{i+1}^{*}$ |
| Out to In | $v_{i}^{*}$ |
| Out to Out |  $\null$ |

where $v^{*}$ represents the intersection of the line segment with the given edge, and that the point $v$ is the one clipped.
