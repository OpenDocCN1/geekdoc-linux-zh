# Chapter 1 : Basic Linux 3D Graphics Concepts

![](bbox=[0.115, 0.09, 0.56, 0.33])

![](bbox=[0.59, 0.09, 1.0, 0.33])

A number of standard operations are defined on vectors. Important for this book are component-wise vector addition, scalar-vector multiplication, the vector dot product, and the vector cross product.

Equation 1-1 
**vector** *v* + **vector** *w* = (*v*_{1}, *v*_{2}, *v*_{3}) + (*w*_{1}, *w*_{2}, *w*_{3}) = (*v*_{1} + *w*_{1}, *v*_{2} + *w*_{2}, *v*_{3} + *w*_{3})

Equation 1-2 
**vector** *v* $\cdot$ *scalar* *s* = (*v*_{1}, *v*_{2}, *v*_{3}) $\cdot$ *s* = (*s* $\cdot$ *v*_{1}, *s* $\cdot$ *v*_{2}, *s* $\cdot$ *v*_{3})

Equation 1-3 
**vector** *v* $\cdot$ **vector** *w* = (*v*_{1}, *v*_{2}, *v*_{3}) $\cdot$ (*w*_{1}, *w*_{2}, *w*_{3}) = (*v*_{1}*w*_{1} + *v*_{2}*w*_{2} + *v*_{3}*w*_{3})

Equation 1-4 
*V* $	imes$ *w* = (*v*_{2}*w*_{3} - *v*_{3}*w*_{2}, *v*_{3}*w*_{1} - *v*_{1}*w*_{3}, *v*_{1}*w*_{2} - *v*_{2}*w*_{1})

# Perspective Projection

Given a coordinate system in which to specify (x,y,z) points, we can then apply a perspective projection to these points to obtain the projected points, for which the seen light rays are identical to those of the original non-projected points. In its simplest form, the perspective projection of a point (x,y,z) is:

Equation 1-5 
*${x}_{p}$* = *${d \frac{x}{z}$* 
*${y}_{p}$* = *${d \frac{y}{z}$*

This formula is derived by computing the intersection between the seen light ray, coming from the point, and a flat 2D projection plane. The *d* term is essentially a scaling factor. A more complete formulation of the perspective projection is:

Equation 1-6 
*${x}_{s}$* = *$\frac{x}{z}(0.5 \cot(0.5\theta) + 0.5) w_{s}$* 
*${y}_{s}$* = *$\frac{y}{z}(0.5 \cot(0.5\theta) w_{s} + 0.5 w_{s}$* 
= *$\frac{y}{z}(0.5 \cot(0.5\theta)) \cdot \frac{w_{s} h_{s} h_{x}}{h_{s} h_{y} w_{s}} + 0.5 scale_{y} h_{s}$* 
= *$\frac{y}{z}(0.5 \cot(0.5\theta)) \cdot \frac{w_{s} h_{s} h_{x}}{h_{s} h_{y} w_{s}} \cdot h_{s} + 0.5 scale_{y} h_{s}$*

This form of the equation explicitly specifies the use of the *d* term as a field of view angle theta. Also, it reverses the *y* axis orientation because it maps the projected points to the 2D pixel