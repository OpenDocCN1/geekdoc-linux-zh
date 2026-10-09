for the current viewpoint (see Chapter 4). Then, for each frame, we only need to draw the polygons that remain in the list.

Each object can update itself. This allows construction of 3D worlds in a modular fashion, with a number of “intelligent” objects capable of acting on their own. An object can update itself by changing its geometry (i.e., altering the vertices in the vertex list), or by applying a transformation matrix to its geometry. Such updates can take place either through sub classing or through plug-ins. With sub classing, a new object subclass overrides the virtual method `update_e`, which updates the object as needed. With a plug-in, we write a dyn amic shared library file which is loaded at run time and which then updates the object.

# Worlds

Just as groups of 3D polygons form a 3D object, groups of 3D objects form a *world*. Class `13d_world` (file `world.h`) is the class we use for storing worlds. A world is a displayable, interactive 3D environment. It contains 3D objects to populate the world, a camera to see the world, a rasterizer to plot pixels, and a screen to display the output.

A simple world as implemented by `13d_world` is really little more than a simple list of objects displayed with the painter’s algorithm. Later, we subclass from `13d_world` to perform more advanced visibility operations on our 3D objects, leading to a graph-like structure of objects connected via portals. See Chapter 5 for details.

For interaction with the external events (such as the user pressing a key on the keyboard), the world class relies on a corresponding pipeline class `13d_pipeline_world` (file `pi_world.h`). The world pipeline class merely forwards events on to the world to be handled.

# Fixed- and Floating-Point Math

In 3D graphics, we generally need to be able to store and manipulate fractional values. For this, we introduce the type `13d_real`. The purpose of the `13d_real` type is to allow all computations using *real* values to be performed using either *floating-point* or *fixed-point* arithmetic. *Floating-point* arithmetic is done by using the C type `float`, and for good real-time performance requires a hardware floating-point unit. *Fixed-point* arithmetic requires no floating-point unit in hardware, and simulates fractional values with integers by multiplying the fractional value so that the fractional part moves into the integer part.

By using `13d_real` any time we want a real value, we can configure our code at compile time to use either fixed- or floating-point math. There are four functions you need to know for using variables of type `13d_real`: