By this point, I'm sure you're painfully aware that although vertical and horizontal lines look good in SVGAlib, diagonal lines leave something to be desired. This is an unfortunate fact of life with the screen matrix system, and it's especially painful in lower-resolution modes. The problem is that there are simply not enough pixels available to represent a diagonal line accurately in most matrices. Therefore, you're left with a rough approximation, complete with jagged edges (or the *jaggies*). This defect, also found in many other systems (that is, it's not intrinsic to Linux or SVGAlib but in fact occurs everywhere you have a screen matrix) is often referred to as *stair-stepping* as well. See Figure 6.2 for an example.

But what's with the name *antialiasing*? A line or shape with rough edges is said to be *aliased*. Therefore, a line or shape that compensates for this flaw has been rendered *antialiased*.

The technique we'll use is to paint some of the jagged object's surrounding pixels to a shade that's in between the object's color and the background color. This provides a sort of make-shift blending effect, and it's quite effective in higher resolutions (that is, in a 640×480 screen mode or higher). Even in low res, it's often better than nothing, although the resultant image may look blurry. Have a look at Figure 6.3 for a better “description”.

# Pedestrian Method

The simplest method for achieving an “antialiased” line (or any other shape) is to merely draw three lines in parallel, with the two bounding lines shaded lighter than the center. For example, suppose you wanted to use color *a* for your line, and the background is color *c*. You would first draw two “buffer” lines shaded in *b*, which is midway between the shades of *a* and *c*. Then, upon placing the center line, you'd have an antialiased effect. You could also draw

![](bbox=[0.11, 0.56, 0.39, 0.72])

![](bbox=[0.11, 0.74, 0.38, 0.9])