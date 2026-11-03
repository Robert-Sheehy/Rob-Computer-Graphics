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


## Worked Example  (graphical)

We'll apply the algorithm to the diagram(s) above


So when clip against the top edge we get

0 to 1 is an example of Out to In so we return $0^{*}$ with is the intersection of the line segment with the edge.

1 to 2 is an example of In to In so we return 1.

2 to 0 is an example of In to Out so we return 2, $0^{@}$

New polygon would be $0^{*} , 1, 2, 0^{@}$

 <img width="700" height="439" alt="image" src="https://github.com/user-attachments/assets/005ead75-1cce-4159-adca-ab0ff13994b6" />

The indices will by default become 0,1,2,3 and will be passed on for processing against the next edge

As before 

0 to 1 is In - In    return 0
1 to 2 is in to Out  return 1, 2*
2 to 3 is Out to In  return 2@
3 to 0 In to In return 3

New polygon will be 0, 1, 2*, 2@, 3

<img width="508" height="316" alt="image" src="https://github.com/user-attachments/assets/666f0c20-15ea-48ec-9aab-ccbc46fa885c" />

Passing on to next edge and renaming a vertices 0,1,2,3,4


| Line Segment| Type | Output |
| :--- | :--- | :--- |
|0-1 | In - In | 0 |
|1-2 | In - In | 1 |
|2-3 | In - In | 2 |
|3-4 | In - Out | 3, $4^{*}$ |
|4-0 | Out - In | $4^{@}$ |


New Polygon 0,1,2,3,$4^{*}, 4^{@}$
<img width="565" height="386" alt="image" src="https://github.com/user-attachments/assets/66d6a3fd-a7da-4bc4-8f40-08cc8b9f8e7c" />

Finally list re-indexed and passed to last edge.




