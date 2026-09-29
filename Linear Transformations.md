# Linear Transformations

The idea behind linnear transformations is that if an object (for our purposes lets say a point or vertex as a 2D or 3D vector) can be represented as the linear combination of a number of bases then we can deduce the image of the point by the following

$(x,y) = x*(1,0) + y*(0,1)$  a general point represented as the linear combnination of the two orthonormal bases $(1,0)$ and $(0,1)$

If we were to examine the folowing diagram   

<img width="1232" height="933" alt="image" src="https://github.com/user-attachments/assets/9dd3a353-8954-4a12-b28c-a8531058799a" />


So $(1,0) \to (cos \theta , sin \theta )$  and $(0,1) \to (-sin\theta , cos \theta) $

This leads to the natural transformation of the point 

$(x,y) = x*(1,0) + y*(0,1) \to x*(cos \theta , sin \theta ) + y*(-sin\theta , cos \theta)$

which means  

$(x,y) \to $ (x*cos\theta$ + y*-sin\theta , x*sin \theta + ycos \theta)$



We have seen that rotation by $\theta$ degrees can be represented by 
```math
R_{\theta} = \begin{pmatrix} \cos\theta & -\sin\theta \\ \sin\theta & \cos\theta \end{pmatrix}
```
We can easily represent scaling with a matrix

```math
S(s_x, s_y) = \begin{pmatrix} s_x & 0 \\ 0 & s_y \end{pmatrix}
```
Unfortunately we cannot use 2x2 matrices to do translation as 
```math
\begin{pmatrix} a & b \\ c & d \end{pmatrix} \begin{pmatrix} 0 \\ 0 \end{pmatrix} = \begin{pmatrix} a \cdot 0 + b \cdot 0 \\ c \cdot 0 + d \cdot 0 \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix}
```

or

 ```math
\begin{pmatrix} 0 & 0 \end{pmatrix} \begin{pmatrix} a & b \\ c & d \end{pmatrix} = \begin{pmatrix} 0 \cdot a + 0 \cdot c & 0 \cdot b + 0 \cdot d \end{pmatrix} = \begin{pmatrix} 0 & 0 \end{pmatrix}
```
This meaans we cannot move the identity, which of course is ususally defined as the centre of every model!!!


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
T(\Delta x, \Delta y) = \begin{pmatrix} 1 & 0 & \Delta x \\ 0 & 1 & \Delta y \\ 0 & 0 & 1 \end{pmatrix}
```

```math
T_{\text{row}}(\Delta x, \Delta y) = \begin{pmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ \Delta x & \Delta y & 1 \end{pmatrix}
```
```math
T_{\text{row}}(\Delta x, \Delta y, \Delta z) = \begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 1 & 0 \\ \Delta x & \Delta y & \Delta z & 1 \end{pmatrix}
```
```math
\text{2D Example:} \quad \begin{pmatrix} x & y & 1 \end{pmatrix} \begin{pmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ \Delta x & \Delta y & 1 \end{pmatrix} = \begin{pmatrix} x \cdot 1 + y \cdot 0 + 1 \cdot \Delta x & x \cdot 0 + y \cdot 1 + 1 \cdot \Delta y & x \cdot 0 + y \cdot 0 + 1 \cdot 1 \end{pmatrix} = \begin{pmatrix} x + \Delta x & y + \Delta y & 1 \end{pmatrix}
```


```math
\text{3D Example:} \quad \begin{pmatrix} x & y & z & 1 \end{pmatrix} \begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 1 & 0 \\ \Delta x & \Delta y & \Delta z & 1 \end{pmatrix} = \begin{pmatrix} x + \Delta x & y + \Delta y & z + \Delta z & 1 \end{pmatrix}
```


```math
S_{\text{col}}(s_x, s_y) = \begin{pmatrix} s_x & 0 & 0 \\ 0 & s_y & 0 \\ 0 & 0 & 1 \end{pmatrix}
```
```math
S_{\text{row}}(s_x, s_y) = \begin{pmatrix} s_x & 0 & 0 \\ 0 & s_y & 0 \\ 0 & 0 & 1 \end{pmatrix}
```
```math
R_{\text{col}}(\theta) = \begin{pmatrix} \cos\theta & -\sin\theta & 0 \\ \sin\theta & \cos\theta & 0 \\ 0 & 0 & 1 \end{pmatrix}
```
```math
R_{\text{row}}(\theta) = \begin{pmatrix} \cos\theta & \sin\theta & 0 \\ -\sin\theta & \cos\theta & 0 \\ 0 & 0 & 1 \end{pmatrix}
```

```math
S(s_x, s_y, s_z) = \begin{pmatrix} s_x & 0 & 0 & 0 \\ 0 & s_y & 0 & 0 \\ 0 & 0 & s_z & 0 \\ 0 & 0 & 0 & 1 \end{pmatrix}
```

```math
R_{x,\text{row}}(\theta) = \begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & \cos\theta & \sin\theta & 0 \\ 0 & -\sin\theta & \cos\theta & 0 \\ 0 & 0 & 0 & 1 \end{pmatrix}
```


