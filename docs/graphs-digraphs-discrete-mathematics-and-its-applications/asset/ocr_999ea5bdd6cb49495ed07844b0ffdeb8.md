equals the number of \(\lambda\)-colorings of \(G\) in which \(u\) and \(v\) are colored differently plus the number of \(\lambda\)-colorings of \(G\) in which \(u\) and \(v\) are colored the same. Since the number of \(\lambda\)-colorings of \(G\) in which \(u\) and \(v\) are colored differently is the number of \(\lambda\)-colorings of \(G + uv\) while the number of \(\lambda\)-colorings of \(G\) in which \(u\) and \(v\) are colored the same is the number of \(\lambda\)-colorings of the graph \(H\) obtained by identifying \(u\) and \(v\), it follows that

\[ P(G,\lambda) = P(G + uv,\lambda) + P(H,\lambda). \]

This observation is summarized below.

# **Theorem 16.10** Let \(G\) be a graph containing nonadjacent vertices \(u\) and \(v\) and let \(H\) be the graph obtained from \(G\) by identifying \(u\) and \(v\). Then

\[ P(G,\lambda) = P(G + uv,\lambda) + P(H,\lambda). \]

Note that if \(G\) is a graph of order \(n \geq 2\) and size \(m \geq 1\), then \(G + uv\) has order \(n\) and size \(m + 1\) while \(H\) has order \(n - 1\) and size at most \(m\).

Of course, the equation stated in Theorem 16.10 can also be expressed as

\[ P(G + uv,\lambda) = P(G,\lambda) - P(H,\lambda). \]

In this context, Theorem 16.10 can be rephrased in terms of an edge deletion and a contraction.

# **Corollary 16.11** Let \(G\) be a graph containing adjacent vertices \(u\) and \(v\) and let \(F\) be the graph obtained from \(G\) by identifying \(u\) and \(v\). Then

\[ P(G,\lambda) = P(G - uv,\lambda) - P(F,\lambda). \]

By systematically applying Theorem 16.10 to pairs of nonadjacent vertices in a graph \(G\), we eventually arrive at a collection of complete graphs whose chromatic polynomials are known. We now illustrate this. Suppose that we wish to compute the chromatic polynomial of the graph \(G\) of Figure 16.21. For the nonadjacent vertices \(u\) and \(v\) of \(G\) and the graph \(H\) obtained by identifying \(u\) and \(v\), it follows by Theorem 16.10 that the chromatic polynomial of \(G\) is the sum of the chromatic polynomials of \(G + uv\) and \(H\).

At this point, it is useful to adopt a convention introduced by Alexander Zыков [263] and utilized later by Read [196]. Rather than repeatedly writing the equation that appears in the statement of Theorem 16.10, we represent the chromatic polynomial of a graph by a drawing of the graph and indicate in the drawing which pair \(u, v\) of nonadjacent vertices will be separately joined by an edge and identified. So, for the graph \(G\) of Figure 16.21, we have the “equation” also shown in Figure 16.21.