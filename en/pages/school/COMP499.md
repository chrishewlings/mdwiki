# COMP 499 

## Images

- An image is a **function** where \\(P = f(x,y)\\)
- Image operations are **functions of functions**

### Filters

- Filters are:
    + **commutative**  : \\(f * g = g * f \\)
    + **associative**  : \\(f * (g*h) = (f*g) * h \\)
    + **distributive** : \\(f * (g+h) = (f*g) * +(f*h) \\)

- Some (but not all!) filters are **separable**, e.g. Gaussian: \\(G_{\sigma}\\) can be separated into \\(G_{\sigma}^{x} * G_{\sigma}^{y} \\)

#### Box Filter

- Averages pixels in neighbourhood (smoothing)

\\[ 
\frac{1}{9} *
\begin{array}{|c|c|c|}
	\hline
	1 & 1 & 1 \\ \hline
	1 & 1 & 1 \\ \hline
	1 & 1 & 1 \\ \hline
\end{array}
\\]

#### Shift Filter

- Moves pixels left or right
- e.g. Shifts image 1px to the **left**:
\\[ 
\begin{array}{|c|c|c|}
	\hline
	0 & 0 & 0 \\ \hline
	0 & 0 & 1 \\ \hline
	0 & 0 & 0 \\ \hline
\end{array}
\\]

#### Sharpening Filter

- Accentuates differences with local average.

\\[ 
\begin{array}{|c|c|c|}
    \hline
    0 & 0 & 0 \\ \hline
    0 & 2 & 0 \\ \hline
    0 & 0 & 0 \\ \hline
\end{array} - 
\frac{1}{9} *
\begin{array}{|c|c|c|}
    \hline
    1 & 1 & 1 \\ \hline
    1 & 1 & 1 \\ \hline
    1 & 1 & 1 \\ \hline
\end{array} = 
\frac{1}{9} *
\begin{array}{|c|c|c|}
	\hline
	-\frac{1}{9} & -\frac{1}{9} & -\frac{1}{9} \\ \hline
	-\frac{1}{9} & \frac{17}{9} & -\frac{1}{9} \\ \hline
	-\frac{1}{9} & -\frac{1}{9} & -\frac{1}{9} \\ \hline
\end{array}
\\]

- Another common sharpening technique is subtracting the 2nd derivative of image from the original.

#### Basic Gradient Filter

\\[
\text{Vertical Gradient: }
\begin{array}{|c|c|c|}
    \hline
    0 & 1 & 0 \\ \hline
    0 & 0 & 0 \\ \hline
    0 & -1 & 0 \\ \hline
\end{array}\hspace{20mm}
\text{Horizontal Gradient: }
\begin{array}{|c|c|c|}
    \hline
    0 & 0 & 0 \\ \hline
    -1 & 0 & 1 \\ \hline
    0 & 0 & 0 \\ \hline
\end{array}
\\]


#### Sobel Filter

- Improves on the basic gradient filter.
- Approximates discrete gradient.
- Often omits the scale term \\(\frac{1}{8}\\) which matters for gradient value but not edge detection.

\\[
\text{Vertical Edge Detector: } 
\begin{array}{|c|c|c|}
    \hline
    1 & 0 & -1 \\ \hline
    2 & 0 & -2 \\ \hline
    1 & 0 & -1 \\ \hline
\end{array}
\hspace{20mm}
\text{Horizontal Edge Detector: } 
\begin{array}{|c|c|c|}
    \hline
    1 & 2 & 1 \\ \hline
    0 & 0 & 0 \\ \hline
   -1 & -2 & -1 \\ \hline
\end{array}
\\]

#### Gaussian Filter

- **Spatially weighted average**. Produces a better smoothing than box filter.
- Two dimensional bell-curve. Can represent the PDF of a normally distributed random variable.
\\[
G_{\sigma} = \frac{1}{Z}e^{\frac{-x^2+y^2}{2\sigma^2}}
\\]
- Parameter \\(\sigma\\) : 'scale', controls amount of smoothing.

\\[
\text{Discrete Approximation: }
\frac{1}{273} *
\begin{array}{|c|c|c|c|c|}
    \hline
    1 & 4 & 7 & 4 & 1 \\ \hline
    4 & 16 & 26 & 16 & 4 \\ \hline
    7 & 26 & 41 & 26 & 7 \\ \hline
    4 & 16 & 26 & 16 & 4 \\ \hline
    1 & 4 & 7 & 4 & 1 \\ \hline
\end{array}
\\]

#### Bilateral Filter

- A Gaussian filter is a spatially weighted, while a bilateral filter is both **space** and **range** weighted and normalized.
- It maintains edges while blurring, whereas a Gaussian does not.

- Parameters:
	+ \\( \sigma_{s} \\): size of neighbourhood
	+ \\( \sigma_{r} \\): minimum edge amplitude

\\[
BF[I]_{p} = \frac{1}{W_{p}} \Sigma G_{\sigma_{s}}(||p - q||)G_{\sigma_{r}}(|I_{p} - I_{q}|)I_{q} 
\\]

#### Laplacian of Gaussian (LoG)

- Looks like an inverted sombrero.
- Laplacian \\(\nabla^2\\) is the sum of the second derivatives of a function.

\\[
\text{Discrete Approximation: }
\begin{array}{|c|c|c|}
\hline
    0 & 1 & 0 \\ \hline
    1 & -4 & 1 \\ \hline
    0 & 1 & 0 \\ \hline
\end{array}
\\]

### Summing rectangular regions (integration)

- Every pixel of the integral image is the sum of itself and its modified N and W neighbours minus its modified NW neighbour, i.e.

\\[
\text{Original image: }
\begin{array}{|c|c|c|}
\hline
    1 & 2 & 3 \\ \hline
    4 & 5 & 6 \\ \hline
    7 & 8 & 9 \\ \hline
\end{array} 
\hspace{10mm} \longrightarrow \hspace{10mm} 
\text{Integral image I: }
\begin{array}{|c|c|c|}
\hline
    1 & 3 & 6 \\ \hline
    5 & 12 & 21 \\ \hline
    12 & 27 & 45 \\ \hline
\end{array} \\[25pt] 
\underline{\text{Generally: }}\\[18pt]
\begin{align*} 
I(x,y) &= I(x,y) + I(x-1,y) + I(x,y-1) - I(x-1,y-1) \\[10pt]
I(x,y) &= I(x,y) + I_{left} + I_{top} - I_{top left}
\end{align*}
\\]

- For any region \\(R\\) with vertices \\(ul,ur,ll,lr\\): 
\\[R_{sum} = ul + lr - ur - ll\\]

## Image Sampling

### Aliasing

- Anomalies that arise when using an insufficent sample rate to sample a continuous signal.
- The **Nyquist rate** is \\(2*f_{max}\\) and is the minimum sampling rate to avoid aliasing.

### Scaling

- **Supersampling/upsampling**: increase image size
- **Subsampling/downsampling**: decrease image size

#### Subsampling

##### Naive subsampling

- Throw away every other row and column --> results in \\( \frac{1}{4}\\) sized image.
- Very fast, but bad results (blurring, moiré)

##### Subsampling with Gaussian pre-filtering

1. Filter the image with a Gaussian mask
2. Perform naive subsampling

n.b. For every iteration, Gaussian mask should **double** in size.

- Continuous iterations of this process form a **Gaussian pyramid** (think mipmaps)
- When fully iterated, a Gaussian pyramid occupies \\( \frac{4}{3} \\) of the original image size.
- Performing \\(L_{i} = G_{i} - expand(G_{i+1}) \\) forms a **Laplacian pyramid**. // TODO

#### Supersampling

- Need to compute the values of pixels at fractional positions. Three approaches:
	- **Nearest neighbour**: pixel is assigned the value of its nearest neighbour.
	- **Bilinear**
	- **Bicubic**: Uses third order curves to improve on bilinear approach.

##### Bilinear Sampling

- Parameters:
	- \\(a\\): horizontal fractional offset 
	- \\(b\\): vertical fractional offset 

\\[
\begin{align*}
f(x+a, y+b) &= (1-a)(1-b)f(x,y) \\
            &+ (a)(1-b)f(x+1,y) \\
            &+ (1-a)(b)f(x,y+1) \\
            &+ (ab)f(x+1,y+1)
\end{align*}            
\\]

## Edge Detection

- Edges are formed by different types of discontinuity:
	+ Surface normal
	+ Depth
	+ Surface color
	+ Illumination
- They can be characterized as points of rapid change of intensity. 
- Noise can interfere greatly with edge detection. Solution? **Smooth first**.

### Gradient

- The **gradient** points in the direction of rapid change in intensity:

\\[
\text{gradient } = \nabla f = [\frac{\partial f}{\partial x}, \frac{\partial f}{\partial x}] 
\\[18pt]
\text{direction } \theta = atan(\frac{\partial f}{\partial y} / \frac{\partial f}{\partial x})
\\[18pt]
\text{magnitude } ||\nabla f|| = \sqrt{(\frac{\partial f}{\partial x})^2 + (\frac{\partial f}{\partial y})^2}
\\]	

### Edge detection by subtraction

Approximates LoG.

1. Take Gaussian
2. Subtract smoothed - original

### Canny

1. Smooth with Gaussian
2. Take gradient
3. Threshold
4. Get orientation at each pixel: \\( \theta = (atan^2(-g_y, g_x) \\)
5. Thinning / non-maximum suppression

- **Non-Maximum suppression** checks if a pixel is a local maximum along the direction of the gradient.

- Higher \\(\sigma\\) for Gaussian will detect larger edges and ignore fine features

### Finding Lines (Hough space)

- A **line** in image space \\((x,y)\\) corresponds to a **point** in Hough space \\((m,b)\\).
- Transform:
	- **Rectangular**: Given a set of points \\((x,y)\\), find all \\((m,b)\\) such that \\(y = mx+b\\).
	- **Polar**: Given a set of points \\((x,y)\\), find all \\((d,\theta)\\) such that \\(d = xcos(\theta) + ysin(\theta)\\).

#### Algorithm

1. Initialize \\(H[d, \theta] = 0 \\)
2. For each edge point \\([x,y]\\) in image:
	- for \\(0 \leq \theta \leq 180 \\):
		- \\(xcos(\theta) + ysin(\theta)\\)
		- \\(H[d,\theta]\\)++
3. Find values of \\((d,\theta)\\) where \\(H[d, \theta]\\) is highest

#### Extensions

1. Use gradient to compute **unique** \\((d,\theta)\\)
2. More votes for stronger edges
3. Higher/lower sampling resolution
4. Different primitives (circles, squares, etc)


## Geometric Transformations

// TODO COPY FROM PAPER NOTES

- **Homogeneous Coordinates**: add another coordinate \\(w\\) to our points/vectors, and divide the others by \\(w\\) when we're done


## Interest Point Operators

- Move a little 'window' across the image
	+ Principle component is the direction of highest variance
	+ Highest component is direction with highest variance **orthogonal** to previous components.

### PCA Algorithm

1. Subtract \\( x - \overline{x} \\) for each data point
2. Compute **covariance matrix**
3. Compute **eigenvectors** and **eigenvalues**
4. Components are the eigenvectors, ranked by the eigenvalues.

#### Covariance

\\[
Covariance(x,y): 
= \frac{1}{n^2} \Sigma_{i}\Sigma_{j>i}(x_{i} - x_{j}) * (y_{i} - y_{j})
\\]

#### Eigenvalues \& Eigenvectors

- Given a matrix \\(A\\):
	- **Eigenvalues** = \\(det(A-\lambda I) = 0\\)
	- **Eigenvectors** are the vectors \\(x\\) that satisfy \\(Ax = \lambda x\\):

\\[
\begin{array}{|cc|}
 h_{11} - \lambda & h_{12} \\
 h_{21} & h_{22} - \lambda
\end{array} \hspace{2mm}
\begin{array}{|c|}
x \\
y 
\end{array}
= 0
\\]

### Harris Corner Detector

- HCD is:
	+ **Translation** invariant
	+ **Rotation** invariant
	+ **Not** scale invariant	

- a.k.a. Second Moment Matrix
\\[
H = \Sigma_{u,v} w(u,v) 
\begin{array}{|cc|}
 I_{x}^{2} & I_{x}I_{y} \\
 I_{x}I_{y} & I_{y}^2 \\
\end{array}
\\]

1. compute \\(I_x,I_y, I_xI_y\\)
2. Apply Gaussian to each
3. Approximate eigenvectors: \\(R = det(H) - \alpha trace(H)^2\\)

Another alternative to approximate eigenvectors is \\( \frac{det(H)}{trace(H)} \\)

#### Scale invariance

- Take Gaussians at multiple spreads and use DoG
- Interest points are local maxima in both position and scale
- Parameter \\(s\\):
	- An **octave** of \\(s+3\\) different spreads of **Gaussian** is formed
	- The **DoG** of the Gaussians are done, giving \\(s+2\\) images

- Keypoints are located by:
	- comparing to 8 neighbours in current image
	- 9 neighbours each in the scales above and below
	- For each extrema found, output is **location** and **scale**

#### Rotation Invariance

- Rotate patch according to its dominant gradient orientation. This ensures patches are in canonical orientation.

## Feature Descriptors

- A **feature vector** describes the neighbourhood around a point of interest by intensities. But it does not deal well with shifts/rotations.

### SIFT descriptors

1. Take a \\(16 \times 16\\) area around a point of interest. This is our **window**
2. Divide the window into a \\(4 \times 4\\) grid of cells
3. Compute an **orientation histogram** for each cell
4. 16 cells * 8 orientations = 128-dimensional descriptor
5. Threshold normalize to a max value of \\(0.2\\)

\\[
\textbf{magnitude: }
\sqrt{ (L(x+1,y) - L(x-1,y))^2 + (L(x,y+1) - L(x,y-1))^2 } \\[18pt]
\textbf{direction } \theta :
atan(\frac{L(x,y+1) - L(x,y-1)}{L(x+1,y) - L(x-1,y)})
\\]

### Other Methods

#### SURF

- Gradient histogram only computed with 4 bins

#### BRIEF

- Randomly sample pixels \\(a,b\\)
- if \\(a > b: 1\text{, else }\\) 0 

### Feature Matching

#### SSD

- Sum of square differences between entried of two descriptors: \\( \Sigma_{i}(f_{1i} - f_{2i})^2 \\)

#### Ratio distance

\\[ \textbf{Ratio distance} = \frac{SSD(f_1,f_2)}{SSD(f_1,f_{2}')} \text{, where } f_{2}' \text{ : 2nd best match}  \\]

### Local Descriptors

- Shapes (log-polar binning)
- Texture (LBP histogram)

#### Bag-of-words
- frequency of occurrences
- Builds a 'visual vocabulary'
- quantize features using visual vocabulary
- represent images by frequencies of 'visual words'

- Issues:
	- **Vocabulary too small**: visual words not representative of all patches 
	- **Vocabulary too large**: quantization artifacts, overfitting
	- **Computational efficiency**: Vocabulary trees

#### Spatial pyramid

- Extends bag-of-words
- Locally orderless representation at several resolutions	

### Viewpoint Invariant (Sivic)

- **Shape Adapted** (SA)
- **Maximal Stable** (MSER)
- Useful for video/film
- Implemented with **K-means clustering**:
	- Regions tracked through contiguous frames, average description computed
	- 10% of tracks with highest variance eliminated
	- Subset of 10% of those shots are selected for clustering
	- Use a distance function (Mahalanobis?) 

- **Clustering** is a common method for learning a visual vocabulary or codebook
	- Each cluster center produces by k-means becomes a **codevector** or visual word
	- The codebook is used for **quantizing features**:
		- A **vector quantizer** takes a feature vector and maps it to the index of the nearest code vector in a codebook

## Image Stitching

### Basic procedure 

1. Take a sequence of images from the same position (rotating around center)
2. Compute transformation between second image and first
	- Extract interest points
	- Find matches
	- Compute transformation 
3. Shift the second image to overlap with the first
4. Blend the two together to create a mosaic
5. Repeat for \\(n\\) images

- Mosaic has a natural interpretation in 3D by projecting images onto a common plane.
- To map a pixel from PP1 to PP2:
	- Cast a ray through each pixel in PP1
	- Draw the pixel where that ray intersects PP2 

	
### Parametrized Coordinate Transformations

- Translation: \\(x' = x + t \\)
- Rotation: \\(x' = Rx + t \\)
- Similarity: \\(x' = sRx + t \\)
- Affine: \\(x' = Ax + t \\)
- Perspective: \\(x' \approx Hx \\), if \\(x\\) is a homogeneous coordinate

### Image Warping

- Given:
	+ coordinate transform \\(x' = h(x)\\)
	+ source image \\(f(x)\\)
	+ transformed image \\(g(x')\\)

- **Forward warping**: 
	+ Send each pixel \\(f(x)\\) to its corresponding location \\(x' = h(x)\\) in \\(g(x')\\)
	+ If source pixel 'lands' between two destinations, add a 'contribution' value and normalize later (splatting)

- **Inverse warping**
	+ Get each pixel \\(g(x')\\) from its corresponding location \\(x' = h(x)\\) in \\(f(x)\\)	
	+ If pixel comes from between two pixels, resample color value from **interpolated** source image

- Transformations:
	+ Translation: 2 DOF
	+ Similarity: 4 DOF
	+ Affine: 6 DOF
	+ Homography: 8 DOF

#### Translation:

\\[ 
\textbf{ displacement of match } i : 
(x'_{i} - x_{i}, y'_{i} - y_{i}) \\[12pt]
\textbf{ Mean displacement } :
(\frac{1}{n} \Sigma_{i=1}^{n} x'_{i} - x_i, \frac{1}{n} \Sigma_{i=1}^{n} y'_{i} - y_i)\\[12pt]
x_i + x_t = x'_i \\
y_i + y_t = y'_i
\\]

- System of equations can be solved with **least squares formulation**.
- For each point, define **residuals**:
\\[
r_{x_{i}}(x_t) = (x_i + x_t) - x'_i \\
r_{y_{i}}(y_t) = (y_i + y_t) - y'_i 
\\]
- Minimize sum of squared residuals:
\\[
C(x_t,y_t) = \Sigma_{i=1}^{n}(r_{x_i}(x_t)^2 + r_{y_i}(y_t)^2)
\\]
- For translations, least squares solution is equal to mean displacement.

##### Least Squares

\\[
\begin{align*}
At &= b \\
A^{T}At &= A^{T}b \\
      t &= (A^{T}A)^{-1}A^{T}b
\end{align*}
\\]

#### Affine 

\\[
x' = ax + by + c \\
y' = dx + ey + f
\\]

Residuals:
\\[
r_{x_i}(a,b,c,d,e,f) = (ax_i + by_i + c) - x'_{i} \\
r_{y_i}(a,b,c,d,e,f) = (dx_i + ey_i + f) - y'_{i} \\
\\]

Cost function:
\\[
C(a,b,c,d,e,f) = \Sigma_{i=1}^{n}(r_{x_i}(a,b,c,d,e,f)^2 + r_{y_i}(a,b,c,d,e,f)^2)
\\]

#### Homographies

- A homography is projective and thus has no scale
- One way of fixing the scale is setting one of the coordinates to 1, but the choice is arbitrary

\\[
x'_{i} = \frac{h_{00}x_i + h_{01}y_i + h_{02}}{h_{20}x_i + h_{21}y_i + h_{22}} \\[18pt]
y'_{i} = \frac{h_{10}x_i + h_{11}y_i + h_{12}}{h_{20}x_i + h_{21}y_i + h_{22}} \\
\\]

- Solve for unit vector \\(h\\) = smaller eigenvector of \\(A^{T}A\\)

- Why can't we solve for homography in same way as affine transform?
	+ Affine transform is a system of equations solvable by linear regression
	+ Homography uses homogeneous coordinates so it only holds up to scale
	+ To make the scale unambiguous, break \\(H\\) into 3 row vectors and divide out the 3rd coordinate to make it 1
	+ Expanding these gives us:
\\[
h_{1}'\overline{x} - y_{i1}h_{3}'\overline{x} = 0 \\
h_{2}'\overline{x} - y_{i2}h_{3}'\overline{x} = 0
\\]
	+ Which can be solved with eigenvector approach

	
#### RANSAC (Random Sample Consensus)

- Estimates homography

1. Select four feature pairs (at random)
2. Compute homography \\(H\\) (exact)
3. Compute inliers where \\(||p_{i}', Hp_{i}|| < \epsilon \\)
4. Repeat
5. Keep largest set of inliers
6. Re-compute least-squares \\(H\\) estimate using all of the inliers

#### Plane Perspective Mosaics

- 8-parameter generalization of affine motion; works for pure rotation or planar surfaces
- Limitations:
	- Local minima
	- slow convergence
	- difficult to control interactively

	