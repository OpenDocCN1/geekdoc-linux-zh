vertex of G is incident with at least 8 green edges. Thus, in the green subgraph H of G, deg_H v ≥ 8 for every vertex v of H which results in deg_H H ∪ deg_H D ≥ 16 for every pair u, v of nonadjacent vertices of H. Since H has no K₅, it follows by Theorem 6.21 that H is pancyclic and so G contains a green C₅. Therefore, R(K₁,₃, K₁,₅, C₅) = 15. ▪

We now determine the Ramsey number of k ≥ 2 graphs, all of which are stars.

# Theorem 20.13
Let s₁, s₂, …, s_k be k ≥ 2 positive integers, t of which are even, and let s = ∑_{i=1}^k (s_i − 1). Then

R(K_{1,s₁}, K_{1,s₂}, …, K_{1,s_k}) = { s + 1 if t is positive and even
s + 2 otherwise }

Proof. Let n = R(K_{1,s₁}, K_{1,s₂}, …, K_{1,s_k}). We consider two cases.

Case 1. t = 0 or t is odd. We show here that n = s + 2. Let there be given a k-edge coloring of K_{s+2} with the colors 1, 2, …, k and let v be a vertex of K_{s+2}. Since deg v = s + 1 = ∑_{i=1}^k (s_i − 1) + 1, it follows that v is incident with at least s_i edges colored i for some i (1 ≤ i ≤ k). Thus, K_{s+2} contains K_{1,s_i} as a subgraph all of whose edges are colored i for some i (1 ≤ i ≤ k). Therefore, n ≤ s + 2.

Next, we show that n ≥ s + 2. First, suppose that t = 0. Then s + 1 is odd and, by Theorem 13.5, the complete graph K_{s+1} can be factored into s/2 Hamiltonian cycles. For i = 1, 2, …, k, let F_i be the (s_i − 1)-factor obtained from (s_i − 1)/2 Hamiltonian cycles. Assigning the color i to each edge in F_i produces a k-edge coloring of K_{s+1} having no subgraph K_{1,s_i}, all of whose edges are colored i. Thus, n ≥ s + 2 and so n = s + 2.

Next, suppose that t is odd. Hence, s + 1 is even and, by Theorem 13.2, the complete graph K_{s+1} can be factored into s = ∑_{i=1}^k (s_i − 1) 1-factors. For i = 1, 2, …, k, let F_i be the (s_i − 1)-factor obtained from (s_i − 1) 1-factors. Assigning the color i to the edges in F_i produces a k-edge coloring of K_{s+1} having no subgraph K_{1,s_i}, all of whose edges are colored i. Thus, n ≥ s + 2 and so n = s + 2.

Case 2. t is positive and even. We show here that n = s + 1. In this case, n = s + 1 = 0. First, we show that n ≤ s + 1. Assume, to the contrary, that there is a k-edge coloring of K_{s+1} containing no subgraph K_{1,s_i}, all of whose edges are colored i, for every i with 1 ≤ i ≤ k. Since every vertex of K_{s+1} has degree s = ∑_{i=1}^k (s_i − 1), it follows that K_{s+1} contains a spanning (s_i − 1)-regular subgraph for every i (1 ≤ i ≤ k). Because some integer s_i − 1 is odd, at least one of these subgraphs has an odd number of odd vertices, which is impossible. Thus, n ≤ s + 1.

Next, we show that n ≥ s + 1. Since t is positive and even, s is even and K_s has a 1-factorization into s − 1 1-factors. We may assume that s_k ≥ 2 is even. Let G_i be the (s_i − 1)-regular spanning subgraph obtained from s_i − 1 of these