or may not be a 2-cell embedding, however. For example, the embedding of \( K_4 \) in Figure 11.9(b) is not a 2-cell embedding. The curves \( C \) and \( C' \) shown in Figures 11.15(a) and 11.15(b) cannot be continuously deformed to a single point in the region in which these curves are drawn. On the other hand, the embedding of \( K_4 \) shown in Figure 11.9(c) and shown again in Figure 11.15(c) is a 2-cell embedding.

![](bbox=[0.1, 0.16, 0.95, 0.26])

Figure 11.15: Non-2-cell and 2-cell embeddings of \( K_4 \) on the torus

# The Generalized Euler Identity

The embeddings of \( K_4 \), \( K_5 \) and \( K_{3,3} \) on a torus given in Figures 11.9(c), 11.10(a) and 11.10(b), respectively, are all 2-cell embeddings. Furthermore, in each case, \( n-m+r=0 \). As it turns out, if \( G \) is a connected graph of order \( n \) and size \( m \) that is 2-cell embedded on a torus resulting in \( r \) regions, then it is always the case that \( n-m+r=0 \). This fact together with the Euler Identity (Theorem 10.1) are special cases of a more general result. The mathematician Simon Antoine Jean Lhuilier spent much of his life working on problems related to the Euler Identity. Lhuilier, like Euler, was from Switzerland and was taught mathematics by one of Euler's former students (Louis Bertrand). Lhuilier saw that the Euler Identity did *not* hold for graphs embedded on spheres containing handles. In fact, he proved a more general form of this identity [156].

> Theorem 11.10 (The Generalized Euler Identity) If \( G \) is a connected graph of order \( n \) and size \( m \) that is 2-cell embedded on a surface of genus \( k \ge 0 \), resulting in \( r \) regions, then
> \[
> n-m+r=2-2k.
> \]

Proof. We proceed by induction on \( k \). If \( G \) is a connected graph of order \( n \) and size \( m \) that is 2-cell embedded on a surface of genus 0, then \( G \) is a plane graph. By the Euler Identity, \( n-m+r=2=2-2 \cdot 0 \). Thus the basis step of the induction holds.

Assume, for every connected graph \( G' \) of order \( n' \) and size \( m' \) that is 2-cell embedded on a surface \( S_k \) for some nonnegative integer \( k \), resulting in \( r' \) regions, that
\[
n'-m'+r'=2-2k.
\]