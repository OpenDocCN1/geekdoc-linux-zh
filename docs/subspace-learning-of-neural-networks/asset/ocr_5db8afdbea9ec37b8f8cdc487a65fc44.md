# 11.3  Simulations

This section includes two examples to illustrate the proposed method.

# 11.3.1  MR-MR Registration

![](bbox=[0.221, 0.234, 0.774, 0.447])

**FIGURE 11.3**  
MR-MR image registration: (a) Reference image and (b) its feature image with threshold 31. (c) Float image and (d) its feature image with threshold 31. (e) Comparison of contours before registration versus (f) after registration

Figure 11.3 shows the result of MR-MR registration. Figure 11.3(a) is used as the reference image, and Figure 11.3(c) is the corresponding float image, which is obtained by a sequential rotation and translation operation with the MRIcro software (http://www.psychology.nottingham.ac.uk). Figure 11.3(b) and 11.3(d) are feature images of Figure 11.3 (a) and 11.3(c), respectively. With PCA neural network, the first principal direction of Figure 11.3(b) is [−0.037, −0.999]ᵀ and that of Figure 11.3(d) is [−0.376, −0.926]ᵀ. Then, by (11.6) and (11.7), the rotation angle is −20.11°. By subtracting the centroid of Figure 11.3(d) from the centroid of Figure 11.3(b), the translations along the x- and y-axis are −1.1 and 8.1 pixels, respectively.

To facilitate the examination of the proposed method, registered image’s contour and reference image’s contour are compared in Figure 11.3(f). Clearly, the two contours almost overlap, which illustrates our method is promising.

# 11.3.2  CT-MR Registration

Images provided in the framework of “The Retrospective Registration Evaluation Project” (http://www.user.virginia.edu/image/registration/) are used in this section. Figure 11.4(a) shows the result of CT-MR registration. Figure