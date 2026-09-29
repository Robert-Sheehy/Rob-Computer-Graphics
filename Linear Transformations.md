# Linear Transformations

The idea behind linnear transformations is that if an object (for our purposes lets say a point or vertex as a 2D or 3D vector) can be represented as the linear combination of a number of bases then we can deduce the image of the point by the following

$(x,y) = x*(1,0) + y*(0,1)$  a general point represented as the linear combnination of the two orthonormal bases $(1,0)$ and $(0,1)$

If we were to examine the folowing diagram   

<img width="1232" height="933" alt="image" src="https://github.com/user-attachments/assets/9dd3a353-8954-4a12-b28c-a8531058799a" />


So $(1,0) \to (cos \theta , sin \theta )$  and $(0,1) \to (-sin\theta , cos \theta) $

This leads to the natural transformation of the point 

$(x,y) = x(1,0) + y(0,1) \to x(\cos\theta, \sin\theta) + y(-\sin\theta, \cos\theta)$

which means

$(x,y) \to (x\cos\theta - y\sin\theta, x\sin\theta + y\cos\theta)$

 Out of this transformation matrix multiplication was born, and this can be done in 2 different ways, depending on whether the matrix representing the transformation is before the point(s) to be trannsformed or after.

If we put the matrix first (Pre-multiply) then the point will be on the right
```math
\begin{pmatrix} \cos\theta & -\sin\theta \\ \sin\theta & \cos\theta \end{pmatrix} \begin{pmatrix} x \\ y \end{pmatrix} = \begin{pmatrix} \cos\theta \cdot x -\sin\theta \cdot y \\ \sin\theta \cdot x + \cos\theta \cdot y \end{pmatrix} 
```

Which is correct according to above..

And if we put the matrix second we call it post mutliplying 

 ```math
\begin{pmatrix} x & y \end{pmatrix} \begin{pmatrix} \cos\theta & \sin\theta \\ -\sin\theta & \cos\theta \end{pmatrix} = \begin{pmatrix} x \cdot \cos\theta + y \cdot -\sin\theta & x \cdot \sin\theta + y \cdot \cos\theta \end{pmatrix} 
```
Again correct accrding to the above.  We can see, and this holds in general, that if we Post multiply, i.e. point on left, matrix on right, the the point is written as a row vector. Conversely, in pre-multiplication, i.e. matrix on left and point on right, the point is writtenn as a column vector.

It is also the case that if you want to convert from one system to the other then the matrices will be the "Transpose" of each other, which means the row of one will be the correspondiong column of the other.


## 🔄 Matrix Transposes & Converting Multiplication Orders

When working across different game engines or shader languages, you will encounter two different ways to multiply matrices and vectors: **Pre-multiplication** (Unity / column vectors) and **Post-multiplication** (Unreal Engine / row vectors). 

To convert an equation from one system to the other without changing the physical transformation result, we use the algebraic property of the **Matrix Transpose** ($M^T$), which flips a matrix over its diagonal (swapping its rows and columns).


### 📐 What is a Matrix Transpose? (A Simple Example)

The **transpose** of a matrix is simply a flipped version of the original matrix. You create it by swapping its **rows** with its **columns**. 

Think of it like spinning the matrix along its top-left-to-bottom-right diagonal axis:
*   Row 1 becomes **Column 1**
*   Row 2 becomes **Column 2**
*   Row 3 becomes **Column 3**

We write the transpose of Matrix $M$ as **$M^T$**.

#### A 2D Transformation Example

Let's look at a basic $2 \times 2$ transformation matrix ($M$) containing simple numbers:

$$
M = \begin{pmatrix} 
{\color{red}1} & {\color{red}2} \\ 
{\color{blue}3} & {\color{blue}4} 
\end{pmatrix}
$$

To find the transpose ($M^T$), we take the first horizontal row $(\color{red}{1, 2})$ and write it as a vertical column. Then we take the second horizontal row $(\color{blue}{3, 4})$ and write it as the second vertical column:

$$
M^{T} = \begin{pmatrix} 
{\color{red}1} & {\color{blue}3}  \\ 
 {\color{red}2} & {\color{blue}4} 
\end{pmatrix}
$$

Notice that the numbers along the main diagonal ($1$ and $4$) stayed exactly where they were, while the off-diagonal numbers ($2$ and $3$) swapped positions.

#### Visualizing Vectors

This same flipping rule applies to coordinate vectors when converting between multiplication styles:

* A vertical **Column Vector** ($v$):

$$ v = \begin{pmatrix} x \\\\ y \end{pmatrix} $$

* Transposing it ($v^T$) turns it into a horizontal **Row Vector**:

$$ v^T = \begin{pmatrix} x & y \end{pmatrix} $$






### The Mathematical Rule

In linear algebra, the transpose of a matrix multiplication reverses the order of the individual parts:

$$ (A \cdot B)^T = B^T \cdot A^T $$

Applying this directly to a transformation vector ($v$) and a transformation matrix ($M$), we can swap between conventions cleanly.

---

### Converting Pre-Multiply to Post-Multiply

#### 1. Pre-Multiplication (Unity Standard)
The matrix stands **before** (to the left of) the vector. The vector is treated as a vertical **column vector**:

$$ v' = M \cdot v $$

#### 2. Converting to Post-Multiplication
If we transpose both sides of the Unity equation to turn our column vector into a horizontal **row vector**, the order flips automatically:

$$ (v')^T = (M \cdot v)^T $$

$$ v'^T = v^T \cdot M^T $$

In the final post-multiplied version, the vector now stands **after** (to the right of) the transposed matrix.

---

### Summary Comparison Matrix

| System | Layout Structure | Vector Type | Used By |
| :--- | :--- | :--- | :--- |
| **Pre-Multiply** | $M \cdot v$ | Column Vector | **Unity**, OpenGL, Shaders (GLSL/HLSL) |
| **Post-Multiply**| $v^T \cdot M^T$ | Row Vector | **Unreal Engine**, Direct3D, Maya |

> ⚠️ **Key Takeaway for Shaders:** If you copy a shader math function written for Unreal Engine into a Unity custom shader, your matrix multiplications will evaluate backwards unless you **transpose the matrix** ($M^T$) and flip the vector to the left side ($v \cdot M$).



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


