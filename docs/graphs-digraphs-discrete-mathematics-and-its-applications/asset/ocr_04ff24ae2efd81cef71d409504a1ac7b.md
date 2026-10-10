# Theorem 8.1

Let u and v be the source and sink, respectively, of a network N with underlying digraph D and let f be a flow defined on N. Then the net flow out of u equals the net flow into v, that is,

f^{+}(u) - f^{-}(u) = f^{-}(v) - f^{+}(v)

# Proof.

Since f^{+}(V(D)) = f^{-}(V(D)), it follows that

\sum_{x \in V(D)} f^{+}(x) = \sum_{x \in V(D)} f^{-}(x). \tag{8.6}

By (8.3),

f^{+}(x) = f^{-}(x) \text{ when } x \neq u, v. \tag{8.7}

By (8.6) then,

f^{+}(u) + f^{+}(v) = f^{-}(u) + f^{-}(v),

giving the desired result. ■

# Maximum Flows

The **value of a flow** f in a network N, denoted by val(f), is defined as the net flow out of the source of N. By Theorem 8.1, val(f) is also the net flow into the sink of N. For the flow f defined on the network in Figure 8.2, we have val(f) = 3.

There are certain flows of particular and obvious interest to us. A flow in a network N whose value is maximum among all flows that can be defined on N is called a **maximum flow**. Thus, a flow f defined on N is a maximum flow if val(f) \geq val(f') for every flow f' defined on N. For a given network, a major goal is to find a maximum flow. For the purpose of doing this, it will be convenient to introduce another concept.