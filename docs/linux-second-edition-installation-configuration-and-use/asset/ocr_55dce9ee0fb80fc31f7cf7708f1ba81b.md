# 20.7 Bezier curves

Of all selection tools presented in this section, BEZIER SELECTIONS (B) are arguably the hardest ones to handle; in return, you will mostly succeed in delimiting the required object with sufficient precision – which is, in spite of all their ease of handling, all other tools fail.

First, a brief mathematical digression: Bezier curves are assembled of pieces of lines of which is described by a third-order polynomial. In practice, this means that for each piece of line, we can specify the start and end points, plus the tangents (that is, the direction) of the curves at these points. The BEZIER tool helps to determine these points together with their tangents.

A Bezier curve is assembled in several steps. Try to familiarize yourself with the tool before you have a go at an elaborate selection – most operations with Bezier curves cannot be undone, so that in case of an error, you have to start all over again.

+   - Set the anchor points of the curve with a series of single mouse clicks. You will need only one anchor point for each piece of curve (ideally where the flexure changes between concave and convex). You close the curve by clicking a second time on the first point.
- Once (the still angular) curve is closed, the left mouse button changes meaning. It now serves to pull the square tangents' control points out of the round anchor points and to modify them.
- Normally, two correlated tangent points lie on one line. However, using Shift together with the mouse button, you can also move the points separately, which gives you more room for creativity. In exchange, the curve gets a kink at the anchor point (whereas otherwise the transition is smooth).
- With Ctrl and the mouse, you can move the anchor points at any time.
- Finally, you click the mouse inside the curve. This converts the Bezier curve into a common selection.

![](bbox=[0.475, 0.645, 0.695, 0.785])

Figure 20.15 A simple Bezier curve.