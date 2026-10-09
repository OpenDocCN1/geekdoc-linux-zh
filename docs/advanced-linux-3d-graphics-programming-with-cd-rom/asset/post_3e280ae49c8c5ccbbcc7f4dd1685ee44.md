
## Specular Reflection

Specular reflection refers to the bright highlights which appear when a shiny surface is illuminated. Such effects are not accounted for by the preceding lighting equations.

![](img/a19d4e8b1d7eb6387691dc6c865430e6_71_0.png)

There are a number of ways of computing the specular reflection. One which we examine here is the so-called Phong illumination model. Do not confuse Phong *illumination*, which deals with the computation of specular light intensities, with Phong *shading*, which refers to a rendering method (covered in the next section) for drawing already computed light intensities.

Phong illumination assumes the surface is shiny and reflective. Therefore, with Phong illumination, we compute a *reflection vector*, which is the reflection of the light vector $L$ (going from the surface to the light source) around the surface normal vector $N$.

![](img/a19d4e8b1d7eb6387691dc6c865430e6_71_1.png)

The idea is that as the orientation of this reflection vector $R$ comes nearer to the orientation of the view vector $V$ (going from the surface to the viewer), the amount of reflected light should increase exponentially, causing a sudden, bright highlight to appear.

Mathematically, we can express Phong illumination as follows. Note that all vector quantities are normalized.

Equation 2-9:
$$I_{spec} = (\cos\alpha)^n = (R \cdot V)^n$$

Thus, the specular intensity increases exponentially as the angle $\alpha$ between the reflection vector and the view vector decreases. The exponential cosine term has this effect; if the vectors lie on top of one another, the cosine is one, and the intensity is at a maximum. As the cosine decreases, the intensity falls off rapidly. The cosine of the angle can be computed by dotting the reflection vector with the view vector. The exponential factor $n$ is a parameter describing the shininess of the surface; the greater the value of $n$, the shinier the surface appears because of an exponentially faster increase and decrease of light intensity around the highlight.

The only issue which remains is how to find the reflection vector. We can calculate the reflection vector by the following equation.

$$R = (2(N \cdot L))N - L$$

The easiest way to derive this is to use the rotation matrix for rotation about an arbitrary axis. Here, we wish to rotate the vector $L$ by 180 degrees about vector $N$. Recall the rotation matrix for rotation about an arbitrary axis:

$$
\begin{bmatrix}
u_1^2 + \cos\theta(1-u_1^2) & u_1u_2(1-\cos\theta) - u_3\sin\theta & u_3u_1(1-\cos\theta) + u_2\sin\theta & 0 \\
u_1u_2(1-\cos\theta) + u_3\sin\theta & u_2^2 + \cos\theta(1-u_2^2) & u_2u_3(1-\cos\theta) - u_1\sin\theta & 0 \\
u_3u_1(1-\cos\theta) - u_2\sin\theta & u_2u_3(1-\cos\theta) + u_1\sin\theta & u_3^2 + \cos\theta(1-u_3^2) & 0 \\
0 & 0 & 0 & 1
\end{bmatrix}
$$

The elements of the matrix are the components of the vector about which the rotation is to take place, in this case $N$. Replacing all $u$ entries with corresponding $N$ entries, multiplying the matrix with the vector $L$ to be rotated, and realizing that the cosine of 180 degrees is -1 and the sine of 180 degrees is 0, gives the following expression:

$$
\begin{bmatrix}
N_1^2 - (1 - N_1^2) & N_1N_2(2) & N_3N_1(2) & 0 \\
N_2N_1(2) & N_2^2 - (1 - N_2^2) & N_2N_3(2) & 0 \\
N_3N_1(2) & N_2N_3(2) & N_3^2 - (1 - N_3^2) & 0 \\
0 & 0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
L_1 \\ L_2 \\ L_3 \\ 0
\end{bmatrix}
$$

Simplifying further yields:

$$
\begin{bmatrix}
2N_1^2 - 1 & 2N_1N_2 & 2N_3N_1 & 0 \\
2N_1N_2 & 2N_2^2 - 1 & 2N_2N_3 & 0 \\
2N_3N_1 & 2N_2N_3 & 2N_3^2 - 1 & 0 \\
0 & 0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
L_1 \\ L_2 \\ L_3 \\ 0
\end{bmatrix}
$$

Performing the matrix multiplication gives us:

$$
\begin{bmatrix}
2N_1^2L_1 - L_1 + 2N_1N_2L_2 + 2N_3N_1L_3 \\
2N_1N_2L_1 + 2N_2^2L_2 - L_2 + 2N_2N_3L_3 \\
2N_3N_1L_1 + 2N_2N_3L_2 + 2N_3^2L_3 - L_3 \\
0
\end{bmatrix}
$$

Notice that each row contains a subtraction with an isolated $L$ term; thus, we can pull out the entire vector $[L_1, L_2, L_3, 0]^T$ and express this as a vector subtraction. We can also isolate the vector $[N_1, N_2, N_3, 0]^T$. Rearranging the equation to be the difference of these two vectors yields the following expression:

$$2(N_1L_1 + N_2L_2 + N_3L_3)[N_1, N_2, N_3, 0]^T - [L_1, L_2, L_3, 0]^T$$

which simplifies to:

Equation 2-16:
$$2(\mathbf{N} \cdot \mathbf{L})\mathbf{N} - \mathbf{L}$$

For a geometrical derivation of the reflection vector, see *Computer Graphics: Principles and Practice* [FOLE92].

Note that unlike diffuse reflection, the effect of which was independent of the viewer position, specular lighting depends on the viewer position, because the position of the highlight changes as the viewer looks at the object from a different angle or position.

**NOTE**

Specular lighting, when it is unwanted, can cause some odd lighting artifacts. I encountered this once while programming a virtual reality application for the CAVE environment (an immersive 3D environment which surrounds the viewer on all sides with four huge screens and provides for true stereoscopic perception and head tracking through special shutter glasses). One odd problem that cropped up was with the floor of a room we had modeled. The surface of the floor appeared to change intensity suddenly when the viewer was located at particular positions within the world. Changing the position, number, and type of light sources did not eliminate the problem. It turned out that the problem was the 3D model exported by the 3D artist included a specular lighting component, which then caused the undesired camera-dependent specular “flashes” of light on the floor. These were particularly problematic because the floor, which was not intended to be specular, was not highly tessellated, meaning that the specular light computation was applied to very large triangles. This caused very large and intermittent white flashes. The solution was to remove the specification of the specular component in the exported 3D model.

## Multiple Light Sources and Components

If we wish to compute the contributions of several light sources to a surface’s illumination, we merely need to compute the light contribution of each light source, then add all the contributions together. Similarly, if we wish to compute lighting based on several light components (for instance, a combination of self-emitted light energy, diffuse reflected light, specular reflection, and ambient light) we also merely need to compute each light contribution separately, then add them all together to arrive at the final light intensity.

One practical problem which may arise is that after summing the light contributions from various sources, the resulting light value may be greater than the maximum allowable intensity of 1.0, which, when multiplied with the integer scaling factor mentioned at the beginning of the discussion on lighting, would yield a lighting table index that would be greater than the maximum allowable index of MAX_LIGHT_LEVELS. In such a case, we can clamp the light intensity to the maximum value, at the cost of some inaccuracy (the intensity should actually be brighter than the maximum possible value). You can see an example of such clamping in Figure 2-11; there, the specular highlight should not be a circle of equal white intensity, instead getting brighter towards its center, but it is impossible for the color on the printed page to increase brighter than pure white. The human eye also has a physically limited maximum input level, so clipping of input light levels also occurs naturally.

## Radiosity and Ray Tracing

Radiosity is a very realistic technique for computing light intensities, based on a physical model of light energy. It works by modeling the physical interaction of light with surfaces, and by ensuring that all of the light energy in a scene is accounted for. Key to the radiosity method is the fact that it also accounts for the illumination resulting from the reflection of light off of surfaces; the previous methods all consider light sources separately from the illuminated surfaces. Radiosity generally works by dividing an entire environment into a number of small patches, each of which is characterized by the amount of light energy it emits or reflects. This implies that all parts of the model can potentially emit light, providing for correct inter-object lighting. The difficult part about radiosity is that the entire lighting solution across all patches must be consistent, meaning that for a large number of patches, a large number of lighting equations must be simultaneously solved to arrive at the correct intensity for each patch. This only makes sense; if each patch can emit light and affect all other patches, which then also emit different amounts of light, a consistent solution requires satisfying the lighting equation for every patch simultaneously. A popular method of computing radiosity is a *progressive refinement* method, where the original model is subdivided into patches only as necessary; if a large change in light intensity is observed for a particular patch, then the patch is subdivided, and the light is recomputed for each small patch.

As realistic as radiosity is, it is slow to compute. Therefore, its role in interactive 3D graphics is more of a pre-processing step. Radiosity can be used in an offline manner to compute light levels, which are then saved along with the 3D geometry. Then, at run time, we simply draw the light using the precomputed light levels.

*Ray tracing* is a rendering technique that can be used to model both reflection and refraction of light. The technique works by tracing the paths of “reverse” light rays from the eye, through each pixel in the image, and to an object in the scene (ordinarily light travels in the other direction, from the objects to the eye). The reverse light rays, like real light rays, are allowed to bounce among objects, and to be refracted after traveling through objects. This means that ray tracing can also create very realistic lighting effects. Ray tracing is currently too slow for real-time applications. See Chapter 7 for more information on ray tracing, and a way of simulating some of the effects of ray tracing through environment mapping.

## Dynamic or Static Lighting Computations

One question we have not addressed is exactly when we carry out the lighting calculations. This answer is partially dependent on the rendering technique we use for drawing the polygons (covered in the next section); it is also partially dependent on whether we want *static lighting* or *dynamic lighting*. Static lighting is lighting which does not change throughout the course of a user’s interaction with the virtual environment. In such a case, we compute light intensities in a preprocessing stage and store these light intensities in some format needed by our rendering technique; storing one color per polygon, or one color per vertex, or one color per lumel in a light map are all possible means of saving the computed light intensities. Then, when drawing the interactive 3D scene, we do not need to worry about computing any light intensities; the light has already been “burned into” or “painted onto” our geometry, and only needs to be drawn using an appropriate rendering technique.
