# FIGURE 23.6

Banner ads help pay
for Web space, but a
small, less-detailed,
quick-loading banner
makes for a more
enjoyable browsing
experience.

![](bbox=[0.223, 0.101, 0.715, 0.323])

# Optimizing Animations

When you build an animation, there are a lot of elements in the picture that are repeated
within every single frame. This is extremely wasteful, repeating the same portions of
animations takes up valuable space and bandwidth. The way to counteract this is
to use only the information that changes from the previous frames in each new frame.

You can improve your animation efficiency by hand simply by cutting out the obvious
unnecessary information. Figure 23.7 illustrates this with the example of a simple, tradi-
tional 88×31 animated Web button. Eliminate the unnecessary by cropping every-
thing that was not within the animated portion after the first frame, which is confined to
a small area in each frame. The animation is then saved with the Make Frame
from Cumulative Layers option, which allows the background frame portions to show
through each frame. This saves a lot of space.

As you can see, this is fairly simple to accomplish when dealing with an animation
which you know that altered portions are taking place within the confines of a small
square (or whatever). But what if the animation has going on throughout the entire
image, as in Figure 23.8? Obviously, it is a bit difficult to determine exactly
what is static and cut it out from the successive frames. Frankly, there is a wonderful
plug-in that can take care of this for you named Animation Optimization. This plug-in is
great because it can find every single pixel that is static after the first frame and cut them
all out! Not only can cut out a few kilobytes (or more, depending on the
file), but can also make it possible to drastically slim down the more complex animations
by reducing them to only the elements that are absolutely necessary, right down to the
abolute value (see Figure 23.9). In this example, I was able to reduce the animation's
size after experimenting with the color depth as well using the Optimization plug-in.
(155k is still definitely not a good size for a Web graphic, but it does illustrate the point.)
Some animations in fact often have greater file size reduction as well (up to 50 percent).