![](bbox=[0.15, 0.12, 0.88, 0.28])

Figure 4.1 Received OFDM signal. P denotes the cyclic prefix with length N_P, and D the information data with length N_D.

preceded by a cyclic prefix P with length N_P ≤ N_D. Assuming that the receiver is not synchronized with the transmitter, we denote by τ the synchronization mismatch, i.e., the epoch of the first sample (in general, 0 ≤ τ ≤ N_P + N_D, with τ = 0 if synchronization is perfect). The total number of samples is N = K(N_P + N_D), and y includes samples from K + 1 OFDM symbols (or K only when τ = 0). We assume that there is no clock drift along the sequence of K symbols. Let d_i denote the N_D-vector of data associated with the i th OFDM symbol x_i. The latter is obtained by concatenating to d_i the last N_P elements of d_i. In vector form,

x_i = U d_i, (4.71)

where U is the (N_P + N_D) × N_D matrix

U ≜ [ 0_{N_P × (N_D - N_P)} I_{N_P} ; I_{N_D} ] . (4.72)

Here, 0_{m×n} denotes the m × n matrix all of whose entries are zero, and I_n the n × n identity matrix. Define further the block-diagonal (K + 1)(N_P + N_D) × (K + 1)N_D matrix consisting of K + 1 copies of U:

T ≜ diag[ U U … U ] . (4.73) K+1

The vector x consisting of K + 1 OFDM symbols is obtained by removing the first τ and the last (N_P + N_D) − τ samples from T d. Thus, we can write

x = T_τ d, (4.74)

where d ≜ [d_1^T d_2^T … d_{K+1}^T]^T, and T_τ is the K(N_P + N_D) × (K + 1)N_D matrix obtained by deleting the first τ and the last (N_P + N_D)−τ rows of T.

# 4.4.1 Neyman–Pearson detection

Invoking the central limit theorem, we assume the data vector d to be white Gaussian, i.e., d ∼ N_c(0, σ_d^2 I), where σ_d^2 is the variance of the complex signal samples. The conditional autocorrelation of x is

E[ x x^T | τ ] = E[ T_τ d d^T T_τ^T ] = σ_d^2 T_τ T_τ^T, (4.75)

so that x | τ ∼ N_c(0, σ_d^2 T_τ T_τ^T). We consider separately the cases of known and unknown values of σ_d^2 and σ_n^2.