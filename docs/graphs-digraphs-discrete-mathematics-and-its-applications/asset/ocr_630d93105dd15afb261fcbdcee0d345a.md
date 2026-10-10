# ## 1.3 Isomorphic Graphs

There is only one graph of order 1, two graphs of order 2, four graphs of order 3 and eleven graphs of order 4. All 18 of these graphs are shown in Figure 1.7. This brings up the question of why every two graphs in Figure 1.7 are considered different. In fact, there is the related question of what it means for two graphs to be considered the same. The technical term for this is *isomorphic graphs* (graphs having the same structure).

![](bbox=[0.15, 0.28, 0.85, 0.45])

Figure 1.7: The (non-isomorphic) graphs of order 4 or less

Two graphs *G* and *H* are **isomorphic** if there exists a bijective function *φ*: *V*(*G*) → *V*(*H*) such that two vertices *u* and *v* are adjacent in *G* if and only if *φ*(*u*) and *φ*(*v*) are adjacent in *H*. The function *φ* is called an **isomorphism** from *G* to *H*. If *φ*: *V*(*G*) → *V*(*H*) is an isomorphism, then the inverse function *φ*⁻¹: *V*(*H*) → *V*(*G*) is an isomorphism from *H* to *G*. If *G* and *H* are isomorphic, we write *G* ≅ *H*. If there is no such function *φ* as described above, then *G* and *H* are **non-isomorphic graphs** and we write *G* ≄ *H*.

The graphs *G* and *H* of Figure 1.8 (both of order 7 and size 8) are isomorphic and the function *φ*: *V*(*G*) → *V*(*H*) defined by

```
φ(u₁) = v₄, φ(u₂) = v₅, φ(u₃) = v₁,
φ(u₄) = v₆, φ(u₅) = v₂, φ(u₆) = v₃, φ(u₇) = v₇
```

is an isomorphism, although there are three other isomorphisms. The graphs *F₁* and *F₂* of Figure 1.8 (both of order 7 and size 10) are not isomorphic however. An explanation of this will be given shortly.

The graphs *G₁* and *G₂* in Figure 1.9 are isomorphic, while *G₁* and *G₃* are not isomorphic. For example, the function *φ*: *V*(*G₁*) → *V*(*G₂*) defined by

```
φ(u₁) = v₁, φ(u₂) = v₃, φ(u₃) = v₅,
φ(u₄) = v₂, φ(u₅) = v₄, φ(u₆) = v₆
```

is an isomorphism. The graph *G₃* of Figure 1.9 contains three mutually adjacent vertices *w₁*,*w₂*,*w₆*. If *G₁* and *G₃* were isomorphic, then for an isomorphism