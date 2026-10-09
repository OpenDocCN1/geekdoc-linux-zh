
This allows for incremental refinement of the model represented by the BSP tree, since a good BSP tree is a multi-resolution bounding of volume.

## Texture LOD Techniques: MIP Mapping

A final type of LOD that deserves mention deals with simplification not of the geometry of an object, but instead of its texture. The reason we wish to do this is to improve the appearance of texture mapped polygons which are viewed from a great distance. In contrast to geometry LOD techniques, which are intended to speed up processing by rendering fewer polygons, this texture LOD scheme mainly aims to improve visual quality. (In some cases this texture LOD scheme can also cause more coherent memory accesses, thus also improving performance, but this is not typically the main goal.)

The problem is that textures viewed at a great distance get mapped onto very few pixels on-screen. With ordinary texture mapping, for each rasterized pixel we only choose exactly one texel from the texture map to display. This causes unwanted moire artifacts, because we are effectively sampling the texture image with too low of a frequency. That is, for a distant texture, several texels should all contribute to the final pixel color on-screen, because several texels all project to the same pixel; but ordinary texture mapping uses just one texel. The plotted color is therefore not representative of the actual light contribution of all texels.

One solution to this problem is to use filtering. This method always dynamically averages the contributions of surrounding texels to arrive at the final pixel color on-screen. This is an excellent solution, but is slow in the absence of hardware support.

Another solution to the problem is to pre-filter the textures into smaller versions, which are used when the polygon is farther away. Then, when performing the texture mapping, we use a texel from the appropriate smaller, pre-filtered texture. We can do this on a per-pixel basis or per-polygon basis. Per-pixel, we compute the distance of each pixel to the camera, select the appropriate texture based on the distance (greater distance causes selection of a smaller texture), then select the appropriate texel from the selected texture. Per-polygon, we simply compute one average distance value for the entire polygon, and then select and apply one entire pre-filtered texture to the polygon, based on the distance. Per-pixel produces better results; per-polygon is faster, but can result in popping artifacts as the entire polygon suddenly shifts between using a smaller and a larger version of the texture.

The smaller, pre-filtered versions of the textures are called MIP maps, although the collection of all such MIP maps is also often referred to as the MIP map. The idea was introduced by Lance Williams in his article “Pyramidal Parametrics” [WILL83]. The MIP in MIP mapping stands for the Latin *multum in parvo*, meaning many things in a small place, which in this case refers to the storage of the original texture and all of its smaller versions in a space 4/3 of the original texture’s size. We arrive at this 4/3 factor as follows. Each smaller version of the texture is typically exactly 1/4 of the size of the original image, having exactly half of the horizontal and vertical dimensions of the next larger version. We can compute such smaller versions simply by averaging the colors from a 4x4 region of the larger version. We continue successively reducing the size of the MIP maps until it is just one pixel wide and/or high. Then, the space requirement expressed as a factor of the original texture size is $1 + 1/4 + 1/16 + 1/64 + 1/256$ and so forth, a series whose limit is $1 + 1/3$, or 4/3.

![](img/a19d4e8b1d7eb6387691dc6c865430e6_525_0.png)

Figure 7-23: A series of MIP maps.

NOTE OpenGL supports MIP mapping; the function `glBuild2DmipMaps` constructs the smaller mipmaps.

## Landscapes

An area of 3D graphics with its own special set of problems and techniques is that of landscapes. This is a unique area due to the storage, generation, and rendering techniques for landscape data. We consider each of these aspects below.

### Storing Landscapes as Height Fields

Landscape data is typically stored as a height field, or elevation grid. A height field is simply an evenly spaced 2D array of values, where each value represents the height of the landscape at that point on the ground. Height fields are a natural and easy way of storing elevation data, and many natural landscapes can be represented with height fields. Those landscapes that cannot be represented with height fields have cliffs or overhangs, where there would be multiple heights for a particular ground location. Fortunately, many natural landscapes do not have such overhangs, since gravity tends to cause overhangs to eventually fall to the earth, thus forming the simple hills and valleys which we can model with height fields.

We can obtain such height field data for real-world locations based on geographical surveying information. For artificial landscapes, we can create the height field by hand in a normal 2D paint program. If we make a 2D gray scale image, then the darker values of gray could represent lower elevations and lighter shades could represent higher elevations. We can then easily and intuitively paint a landscape, as if we were viewing it from above.

We can use tiles to reduce the memory requirements of a large landscape. The idea is to create several small landscape maps, all of which match on the edges. Then, by combining these tiles in various ways, we can generate varied landscapes with reduced storage requirements. Of course, such a scheme introduces repetition into the landscape, but clever arrangement of the tiles can hide this fact. Also, using the same tiles at different elevations is an effective reuse technique. To reuse a tile at different elevations, the geometry within the tile would need to slope upwards or downwards, so that the tiles match up seamlessly on the edges.

### Generating Fractal Landscapes

Height field data for landscapes can also be generated algorithmically. Perhaps the best known class of algorithms for generating such data are the fractal algorithms. Fractal landscape algorithms fundamentally work by starting with a single, undivided polygon. The polygon is then divided into smaller polygons, which adds new vertices. The new vertices are first positioned at the average height of their neighboring vertices, then are additionally randomly displaced up or down. We recursively repeat the subdivision, with the important property that the amount of random displacement gets smaller and smaller as we divide further and further. This means that the first few coarse levels of subdivision establish large-scale hills and valleys; increasing subdivision leads to finer and finer surface details. The exact reason this works is because the random displacements simulate Brownian motion in two dimensions, creating a surface with fractal dimension [PEIT92]. Fractal dimension means that the surface has a fractional dimension between 2D and 3D (hence the term fractal) and appears self-similar. The specific factor by which the amount of displacement is reduced for each recursive subdivision depends on this fractal property, and for square polygons is $\sqrt{1/2^{2h}}$, where $h$ is the level of recursion. See [PEIT92] for the derivation and an extremely broad introduction to the field of fractals and chaos theory.

You can program a fractal landscape generator without too much difficulty based on the previous description. Also, Blender has a fractal subdivision option which you can use to experiment. To try this in Blender, add a plane and remain in EditMode. Then type w, and select Subdivide Fractal to subdivide all selected vertices in a fractal manner. By repeating this process, you can create more and more fractal landscape detail. Blender, however, only allows you to access and export the data as a polygonal mesh, not as a 2D height field.

![](img/a19d4e8b1d7eb6387691dc6c865430e6_526_0.png)

Figure 7-24: A Blender mesh subdivided in a fractal manner.
