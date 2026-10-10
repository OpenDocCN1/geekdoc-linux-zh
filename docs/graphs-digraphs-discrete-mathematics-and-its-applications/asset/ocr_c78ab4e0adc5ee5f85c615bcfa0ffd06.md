![](bbox=[0.23, 0.08, 0.83, 0.32])

Figure 3.15: Two spanning trees T₁ and T₂ in a graph

If *u* and *v* are two nonadjacent vertices of a tree *T₀*, then *T₀* + *uv* contains exactly one cycle *C* and the cycle *C* contains the edge *uv*. For any edge *xy* belonging to *C*, the graph *T₁* = *T₀* + *uv* − *xy* is again a tree. The tree *T₀* is said to be transformed into *T₁* by an **edge exchange**. This transformation from *T₀* to *T₁* is illustrated in Figure 3.16.

![](bbox=[0.13, 0.48, 0.87, 0.6])

Figure 3.16: Transforming a tree T₀ into a tree T₁ by an edge exchange

**Theorem 3.25** Let *G* be a connected graph. If *G* contains a spanning tree with exactly *r* leaves and a spanning tree with exactly *t* leaves where *r* < *t*, then for every integer *s* with *r* < *s* < *t*, there is a spanning tree of *G* with exactly *s* leaves.

**Proof.** Let *T₀* be a spanning tree of *G* with *r* leaves and let *T* be a spanning tree of *G* with *t* leaves. Clearly, *E(T₀)* ≠ *E(T)*. Let *e* be an edge of *T* not belonging to *T₀*. Then *T₀* + *e* is a unicyclic graph whose cycle *C* contains an edge *f* not belonging to *T*. Thus *T₀* is transformed into the spanning tree *T₁* = *T₀* + *e* − *f* by an edge exchange where *T₁* has one more edge in common with *T* than *T₀* does. If *T₁* = *T*, then the transformation is complete; otherwise, *T₁* can be transformed into a spanning tree *T₂* having one more edge in common with *T* than *T₁* does. We continue this until we arrive at *T*, that is, we have a sequence

*T₀, T₁, T₂, …, Tₖ = T*

of spanning trees of *G* where for each *i* (1 ≤ *i* ≤ *k*), *Tᵢ₋₁* is transformed into *Tᵢ* by an edge exchange and *Tᵢ* has one more edge in common with *T* than *Tᵢ₋₁*