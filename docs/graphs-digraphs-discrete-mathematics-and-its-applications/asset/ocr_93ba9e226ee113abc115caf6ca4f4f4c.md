# Theorem 18.7 For an integer k \u2265 2, a bridgeless plane graph G is k-region colorable if and only if G has a nowhere-zero k-flow.

Proof. First, let there be given a k-region coloring c of G and let D be an orientation of G. For each arc e = (u, v) of D, let R\u2081 be the region of G that lies to the right of e and R\u2082 the region of G that lies to the left of e. Define an integer-valued function \u03d5 of E(D) by

\u03d5(e) = c(R\u2081) \u2212 c(R\u2082).

We show that \u03d5 is a nowhere-zero k-flow. Since uv is not a bridge of G, c(R\u2081) \u2260 c(R\u2082) and since 1 \u2264 c(R) \u2264 k for each region R of G, it follows that

\u03d5(e) \u2208 {\u00b11, \u00b12, \u2026, \u00b1(k \u2212 1)}.

It remains only to show that \u03c3\u207a(v; \u03d5) = \u03c3\u207b(v; \u03d5) for each vertex v of D. Suppose that deg\u2098 v = t and that v\u2081, v\u2082, \u2026, v\u1d52 are the neighbors of v as we proceed cyclically about v in some direction. For i = 1,2,\u2026,t, let R\u1da0 denote the region having v\u1da0 and v\u1da0+1 on its boundary where v\u1da0+1 = v\u2081. Thus, in D each edge v\u1da0v\u1da0+1 (1 \u2264 i \u2264 t) is either the arc (v\u1da0, v\u1da0+1) or the arc (v\u1da0+1, v\u1da0). Let c(R\u1da0) = c\u1da0, for i = 1,2,\u2026,t. Let j \u2208 {1,2,\u2026,t} and consider c(R\u1da0) = c\u1da0. If \u27e8(v, v\u1da0), (v, v\u1da0+1) \u2208 E(D), then c\u1da0 and \u2212c\u1da0 occur in \u03c3\u207a(v; \u03d5) and c(R\u1da0) does not occur in \u03c3\u207b(v; \u03d5). The situation is reversed if (v\u1da0, v), (v\u1da0+1, v) \u2208 E(D). If (v, v\u1da0+1), (v\u1da0, v) \u2208 E(D), then the term c\u1da0 occurs in both \u03c3\u207a(v; \u03d5) and \u03c3\u207b(v; \u03d5); while, if (v\u1da0+1, v), (v, v\u1da0) \u2208 E(D), then the term \u2212c\u1da0 occurs in both \u03c3\u207a(v; \u03d5) and \u03c3\u207b(v; \u03d5). Thus,

\u03c3\u207a(v; \u03d5) = \u03c3\u207b(v; \u03d5)

and \u03d5 is a nowhere-zero k-flow.

Next, suppose that G is a bridgeless plane graph having a nowhere-zero k-flow. This implies that for a given orientation D of G, there exists a nowhere-zero k-flow \u03c6 of D. By definition then, \u03c3\u207a(v; \u03c6) = \u03c3\u207b(v; \u03c6) for every vertex v of D.

We now consider directed closed curves in the plane that do not pass through any vertex of D. Such closed curves may enclose none, one or several vertices of G. For a directed closed curve C, we define the number \u03c3(C; \u03c6) to be the sum of terms \u03c6(e) or \u2212\u03c6(e) for each occurrence of an arc e crossed by C. In particular, as we proceed along C in the direction of C and cross an arc e, we contribute \u03c6(e) to \u03c3(C; \u03c6) if e is directed to the right of C and contribute \u2212\u03c6(e) to \u03c3(C; \u03c6) if e is directed to the left of C.

If C is a directed simple closed curve in the plane that encloses no vertex of D, then for each occurrence of an arc e crossed by C that is directed to the right of C, there is an occurrence of e crossed by C that is directed to the left of C. Hence, in this case, \u03c3(C; \u03c6) = 0. If C encloses a single vertex v, then because \u03c3\u207a(v; \u03c6) = \u03c3\u207b(v; \u03c6), it follows that \u03c3(C; \u03c6) = 0 here as well. (See Figure 18.5 for example.)