extensively studied and used in many fields; see examples [3, 20, 22, 23, 97, 106, 108, 138, 169].

# ### 1.1.3　Outline of This Book

The rest of this chapter is organized as follows. In Section 2, the methods for convergence analysis is introduced and the relationship between SDT algorithm and the corresponding DDT algorithm is given in Section 3. Section 4 presents some notations and preliminaries.

In Chapter 2, the convergence of Oja’s and Xu’s algorithms with constant learning rates is studied in detail. Some invariant sets are obtained and local convergence is proven rigorously. The most important contribution is the convergence analysis framework of deterministic discrete time (DDT) method is established in this chapter.

In Chapter 3, an adaptive learning rate is provided for the subspace learning algorithms. The global boundedness of Oja’s algorithm with the adaptive learning rate is analyzed first. Then, the global convergence conditions are obtained.

In Chapter 4, the convergence of Generalized Hebbian Algorithm (GHA) is studied via the DDT method. GHA can extract multiple principal component directions in parallel. In this chapter, mathematical induction is used to prove the global convergence of GHA with adaptive learning rates.

In Chapter 5, a stable MCA algorithm is proposed, and its dynamics of the proposed algorithm is interpreted indirectly by using DDT method.

In Chapter 6, the Hyvärinen-Oja’s ICA learning algorithm is discussed. The corresponding DDT algorithms are extended to the block versions of the original SDT algorithms. The block algorithms not only establish a relationship between the SDT algorithms and the corresponding DDT algorithms, but also can get a good convergence speed and accuracy in practice.

In Chapter 7, chaotic behaviors of subspace learning algorithms are presented. It will be shown that some algorithms have both stability and chaotic behavior under some conditions. This chapter explores the chaotic behavior of a class of ICA algorithms. The conditions for stability and chaos of the algorithm are derived.

In Chapter 8, a biologically plausible PCA model is proposed to adaptively determine the number of principal component directions. The number adaptively approximates the intrinsic dimensionality of the given data set by using an improved GHA. Some simulations are conducted to verify the theoretical results.

In Chapter 9, an adaptive learning rate is proposed to guarantee the global convergence of Oja’s MCA algorithm. Then, a multi-block-based MCA method is used for nonlinear surface fitting. The method shows good performance in terms of accuracy, which is confirmed by the simulation results.

In Chapter 10, an ICA algorithm is proposed for extracting fetal electro-