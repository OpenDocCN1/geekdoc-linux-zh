# ## Exercises for Chapter 5

# **Section 5.1. The Königsberg Bridge Problem**

+   1. In present-day Königsberg (Kaliningrad), there are two additional bridges, one between regions B and C and one between regions B and D. Is it now possible to devise a route over all bridges of Königsberg without recrossing any of them?

+   2. Euler's approach to solve the Königsberg Bridge Problem was to observe that if there was a route that crossed each of the seven bridges exactly once, then this route could be represented by a sequence of eight letters, where each term represents a land region to which the route had progressed and each of the seven pairs of consecutive letters in the sequence represents a bridge that the route had crossed. Another observation that Euler could have made was that there are at least two land regions that were neither the beginning nor the end of such a route. Show that this observation could be used to solve the Königsberg Bridge Problem.

+   3. Suppose that the Königsberg Bridge Problem had asked instead whether it was possible to take a route about Königsberg that crossed each bridge exactly twice. What would have been the answer in this case?

+   4. Suppose that there is a boat in Königsberg that moves along the River Pregel and travels under its bridges. In such a boat ride, a boat travels under each bridge at most once. What is the maximum number of bridges under which a boat can travel?

# **Section 5.2. Eulerian Circuits and Trails**

+   5. Let *F* and *H* be two disjoint connected non-Eulerian regular graphs and let *G* = (*F* + *H*) ∨ *K*<sub>1</sub>; that is, *G* is obtained from *F* and *H* by adding a new vertex *v* and joining *v* to each vertex in *F* and *H*. Prove that *G* is Eulerian.

+   6. Let *G* be a connected graph of order *n* ≥ 4 that has neither an Eulerian circuit nor an Eulerian trail. A graph *H* is constructed by adding a new vertex *v* to *G* and joining *v* to every odd vertex of *G*. Prove or disprove: *H* is Eulerian.

+   7. Find a necessary and sufficient condition for the Cartesian product *G* □ *H* of two nontrivial connected graphs *G* and *H* to be Eulerian.

+   8. Prove that if a graph of order *n* ≥ 6 has an Eulerian *u* – *v* trail such that deg *u* – deg *v* ≥ *n* – 2, then *n* must be even.