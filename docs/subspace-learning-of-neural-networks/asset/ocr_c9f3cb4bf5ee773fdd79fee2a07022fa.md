This chapter is organized as follows. Section 2 provides the problem formulation and gives preliminaries. Convergence results are given in Section 3. The DDT algorithms are extended to the block algorithms in Section 4. Simulation results and discussions are presented in Section 5. Conclusions are drawn in Section 6.

# 6.2  Preliminaries and Hyvärinen-Oja’s Algorithms

Suppose a sequence of observations {y(k), k = 1, 2, …} with m scalar random variables, that is, y(k) = [y₁(k), y₂(k), …, yₘ(k)]ᵀ. In the simplest of ICA [49], it is assumed that

$$\mathbf{y}(k)=\mathbf{A}\mathbf{s}(k),$$

where s(k) = [s₁(k), s₂(k), …, sₙ(k)]ᵀ is unknown and s₁(k), s₂(k), …, sₙ(k) are mutually and statistically independent with zero mean and unit variance. A is an unknown m × n mixing matrix of full rank. The basic problem of ICA is then to estimate the original s(k) from the mixtures y(k). The problem can be simplified by prewhitening of the data y(k). The observed data y(k) is linearly transformed to a vector x = My such that its elements xᵢ are mutually uncorrelated and all have unit variance, that is, E{x(k)xᵀ(k)} = I. It follows that

$$\mathbf{x}(k)=\mathbf{M}\mathbf{y}(k)=\mathbf{M}\mathbf{A}\mathbf{s}(k)=\mathbf{B}\mathbf{s}(k),$$

where B is an orthogonal matrix. Clearly, E{x(k)xᵀ(k)} = BE{s(k)sᵀ(k)}Bᵀ = BBᵀ = I, where B = (b₁, b₂, …, bₙ), sᵢ(k) = bᵢᵀx(k). Then, the problem of ICA is transformed to one of estimating the bᵢ.

The kurtosis of the signals is usually used to solve the ICA problem [85, 86, 87]. As for a zero mean random variable v, the kurtosis is defined as Kurt(v) = E{v⁴} − 3E{v²}². It is easy to show that Kurt(v₁ + v₂) = Kurt(v₁) + Kurt(v₂) and Kurt(αv₁) = α⁴Kurt(v₁), where v₁ and v₂ are two independent, zero mean random variables.

For the signals s₁(k), s₂(k), …, sₙ(k), denote by Kurt(sᵢ) the kurtosis of the signal sᵢ(k). Clearly, Kurt(sᵢ) = E{sᵢ⁴(k)} − 3. Define some sets as follows: P = {i|Kurt(sᵢ) < 0, i ∈ {1, 2, …, n}}, Q = {i|Kurt(sᵢ) > 0, i ∈ {1, 2, …, n}}, O = {i|Kurt(sᵢ) = 0, i ∈ {1, 2, …, n}} and T = O ∪ P ∪ Q.

Let V_q be the subspace spanned by {bᵢ|Kurt(sᵢ) > 0}, that is, V_q = span{bᵢ|Kurt(sᵢ) > 0}. The subspace V_q^⊥ is perpendicular to V_q. Let V_p = span{bᵢ|Kurt(sᵢ) < 0} and V_p^⊥ is perpendicular to V_p.

To estimate the direction of bᵢ, in [87], Hyvärinen and Oja proposed the ICA learning algorithms with

$$\mathbf{w}(k+1)=\mathbf{w}(k)+\mu(k)\left[\sigma\mathbf{x}(k)f\left(\mathbf{w}^{T}(k)\mathbf{x}(k)\right)+a\left(1-\lVert\mathbf{w}(k)\rVert^{2}\right)\mathbf{w}(k)\right],$$

for all k ≥ 0 and a > 0, where f is a scalar function, and σ = ±1 is a sign that