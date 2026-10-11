can use a very powerful Linux computer to create 3D models of buildings, but display those models using much less powerful computers equipped with suitable 3D graphics cards. The two computers need not even run the same OS. If you're used to dealing with X in a networked environment, this concept should be familiar.

Several different OpenGL implementations for Linux exist:

+   - **Mesa**  This implementation, available from `http://mesa3d.sourceforge.net`, is not officially an implementation of OpenGL for Linux. It is, rather, "very similar to... OpenGL," according to the Web site's opening page. Many OpenGL programs work quite well using Mesa, and it can be an acceptable replacement for OpenGL for many users.

+   - **Xi Graphics' 3D Accelerated-X**  Xi Graphics (`http://www.xig.com`) has released a version of its Accelerated-X commercial X server that includes OpenGL support. This product supports a variety of 3D graphics cards and includes code licensed from SGI.

+   - **Metrolink OpenGL**  Another competitor in the commercial X server market for Linux, Metrolink (`http://www.metrolink.com`) offers a package that includes the Metro-X server and an OpenGL implementation. Like Xi Graphics' product, Metrolink's OpenGL uses code licensed from SGI.

Whatever form of OpenGL you use, the result is an ability to create 3D images with relatively little programming effort. Figure 12.2 shows a simple example, produced by a demo program included with Mesa. OpenGL is likely to be used by many applications in the future, as more and more serious applications find uses for 3D graphics.

![](bbox=[0.39, 0.58, 0.69, 0.82])

# FIGURE 12.2

OpenGL lets you create 3D geometric images, animate them, and combine them with other images.