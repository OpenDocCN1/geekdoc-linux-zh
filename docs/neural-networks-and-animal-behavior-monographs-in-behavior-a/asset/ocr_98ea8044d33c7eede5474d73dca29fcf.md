![](bbox=[0.24, 0.13, 0.72, 0.3])

Figure 2.9 An error surface for a network with two weights. For a given task, the height of the surface at (W₁, W₂) is the error E(W₁, W₂) relative to this particular choice of weights.

It can be shown that this vector points in the direction of steepest ascent. To descend the error surface, one thus should travel in the opposite direction. Additionally, the steps should not be too long: since the path to follow generally will be curved, the direction of travel needs to be updated regularly. This reasoning is formalized by writing the update ΔWᵢ to weight Wᵢ as

```
ΔWᵢ = -η∇ᵢE(W) (2.35)
```

where ∇ᵢE(W) is the iᵗʰ component of the gradient vector (i.e., the derivative of E(W) with respect to Wᵢ), and η is a small positive number that calibrates step length. Once equation (2.35) has been applied to all weights, the gradient is calculated anew, then equation (2.35) is applied once more, and so on until error has decreased to a satisfactorily low figure. That is, gradient descent is an *iterative procedure*, and equation (2.35) is applied at each iteration. Note that although we started from an example with only two weights, equation (2.35) can be applied to networks with an any number of weights.

We must consider two important complications that are not apparent in Figure 2.9. In fact, the figure portrays a particularly favorable case where the error surface has a unique minimum, and the gradient always points in a direction that leads to the minimum along a rather short path. In general, neither is guaranteed to hold. The error surface may have many minima, of which only one or a few are satisfactory. Moreover, following the gradient may result in a very long path, which could be avoided with a fuller knowledge of the error surface. In defense of gradient methods, we can say that taking the path of steepest descent is a reasonable thing to do having only *local* information about the error surface (e.g., about how the error would change if the weights were changed slightly from their current values). The basic algorithm presented here can be improved in many ways, as explained, for instance, in Haykin (1999) and Golden (1996).