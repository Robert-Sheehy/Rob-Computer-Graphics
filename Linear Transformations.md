# Linear Transformations

We have seen that rotation by $\theta$ degrees can be represented by 
```math
R\((\theta) = \begin{bmatrix} \cos\theta & -\sin\theta \\ \sin\theta & \cos\theta \end{bmatrix}\)
```
We can easily represent scaling with a matrix

```math
S(s_x, s_y) \(= \begin{bmatrix} s_x & 0 \\ 0 & s_y \end{bmatrix}\)
```
Unfortunately we cannot use 2x2 matrices to do translation as 
```math
\(\begin{bmatrix} a & b \\ c & d \end{bmatrix} \begin{bmatrix} 0 \\ 0 \end{bmatrix} = \begin{bmatrix} a \cdot 0 + b \cdot 0 \\ c \cdot 0 + d \cdot 0 \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \end{bmatrix}\)
```

or

 ```math
\(\begin{bmatrix} 0 & 0 \end{bmatrix} \begin{bmatrix} a & b \\ c & d \end{bmatrix} = \begin{bmatrix} 0 \cdot a + 0 \cdot c & 0 \cdot b + 0 \cdot d \end{bmatrix} = \begin{bmatrix} 0 & 0 \end{bmatrix}\)
```

For this reason we introduce.....

## Homogeneous Coordinates

### Definition

#### Simple version

$(x,y) \to (x,y,1)$
and $(x,y,z) \to (x,y,z,1)$

#### Actual definition

$(x,y) \to (wx,wy,w)$
and $(x,y,z) \to (wx,wy,wz,w)$


```math
T\((\Delta x, \Delta y) = \begin{bmatrix} 1 & 0 & \Delta x \\ 0 & 1 & \Delta y \\ 0 & 0 & 1 \end{bmatrix}\)
```

```math
\(T_{\text{row}}(\Delta x, \Delta y) = \begin{bmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ \Delta x & \Delta y & 1 \end{bmatrix}\)
```
```math
\(T_{\text{row}}(\Delta x, \Delta y, \Delta z) = \begin{bmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 1 & 0 \\ \Delta x & \Delta y & \Delta z & 1 \end{bmatrix}\)
```
```math
\(\text{2D Example:} \quad \begin{bmatrix} x & y & 1 \end{bmatrix} \begin{bmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ \Delta x & \Delta y & 1 \end{bmatrix} = \begin{bmatrix} x \cdot 1 + y \cdot 0 + 1 \cdot \Delta x & x \cdot 0 + y \cdot 1 + 1 \cdot \Delta y & x \cdot 0 + y \cdot 0 + 1 \cdot 1 \end{bmatrix} = \begin{bmatrix} x + \Delta x & y + \Delta y & 1 \end{bmatrix}\)
```


```math
\(\text{3D Example:} \quad \begin{bmatrix} x & y & z & 1 \end{bmatrix} \begin{bmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 1 & 0 \\ \Delta x & \Delta y & \Delta z & 1 \end{bmatrix} = \begin{bmatrix} x + \Delta x & y + \Delta y & z + \Delta z & 1 \end{bmatrix}\)
```


```math
\(S_{\text{col}}(s_x, s_y) = \begin{bmatrix} s_x & 0 & 0 \\ 0 & s_y & 0 \\ 0 & 0 & 1 \end{bmatrix}\)
```
```math
\(S_{\text{row}}(s_x, s_y) = \begin{bmatrix} s_x & 0 & 0 \\ 0 & s_y & 0 \\ 0 & 0 & 1 \end{bmatrix}\)
```
```math
\(R_{\text{col}}(\theta) = \begin{bmatrix} \cos\theta & -\sin\theta & 0 \\ \sin\theta & \cos\theta & 0 \\ 0 & 0 & 1 \end{bmatrix}\)
```
```math
\(R_{\text{row}}(\theta) = \begin{bmatrix} \cos\theta & \sin\theta & 0 \\ -\sin\theta & \cos\theta & 0 \\ 0 & 0 & 1 \end{bmatrix}\)
```

```math
\(S(s_x, s_y, s_z) = \begin{bmatrix} s_x & 0 & 0 & 0 \\ 0 & s_y & 0 & 0 \\ 0 & 0 & s_z & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix}\)
```

```math
R_{x\(,\text{row}\)}\((\theta) = \begin{bmatrix} 1 & 0 & 0 & 0 \\ 0 & \cos\theta & \sin\theta & 0 \\ 0 & -\sin\theta & \cos\theta & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix}\)
```


