![](bbox=[0.13, 0.1, 0.41, 0.3])

![](bbox=[0.44, 0.1, 0.72, 0.3])

![](bbox=[0.13, 0.33, 0.41, 0.53])

![](bbox=[0.44, 0.33, 0.72, 0.53])

Figure 3-16: Moving the effector of the Ika chain causes the rest of the chain to automatically follow.

Figure 3-17: Moving the base of an Ika moves the entire Ika.

Just remember the following in order to distinguish between inverse and forward kinematics: In inverse kinematics, you move the lowest item in a hierarchy (the effector), which automatically successively moves all higher items in the hierarchy. In forward kinematics, you explicitly start at the highest level in the hierarchy, and successively manually move the lower items in the hierarchy, which finally determines the position of the lowest item in the hierarchy. Inverse kinematics works from the bottom up; forward kinematics works from the top down.

The choice of which is more appropriate— inverse kinematics or forward kinematics—depends on the most convenient way you like to think about the animation process. Generally, it’s easier to think of limb animation in terms of inverse kinematics. For instance, when animating an arm, you usually think of the animation in terms of moving the hand (the effector) towards an object, and not in terms of moving the upper and lower arms individually. But since inverse kinematics automatically recalculates the joint positions, it also gives you less control over the exact animation. When animating a tail or a snake with many segments, it might be better to use forward kinematics.

For this tutorial, we’ll use IK for animating the arms and legs of a human-like figure to create a simple walking motion. The first step is to understand how to create and manipulate IKas in Blender.