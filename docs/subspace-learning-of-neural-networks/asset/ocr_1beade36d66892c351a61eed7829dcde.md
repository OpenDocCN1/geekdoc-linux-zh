Proof: From (1.8), (2.13), we have

wᵀ(k + 1)Cw(k + 1) = ∑ᵢ₌₁ⁿ λᵢ [1 + η(λᵢ(2 − ‖w(k)‖²) − wᵀ(k)Cw(k))]² zᵢ²(k)

= ∑ᵢ₌₁ⁿ λᵢ [1 + η(σ(2 − ‖w(k)‖²) − wᵀ(k)Cw(k))]² zᵢ²(k) + ∑ᵢ₌ₘ₊₁ⁿ λᵢ [1 + η(λᵢ(2 − ‖w(k)‖²) − wᵀ(k)Cw(k))]² zᵢ²(k) − ∑ᵢ₌ₘ₊₁ⁿ λᵢ [1 + η(σ(2 − ‖w(k)‖²) − wᵀ(k)Cw(k))]² zᵢ²(k)

= [1 + η(σ(2 − ‖w(k)‖²) − wᵀ(k)Cw(k))]² · wᵀ(k)Cw(k) − Q(k)

for k ≥ 0, where

Q(k) = η ∑ᵢ₌ₘ₊₁ⁿ λᵢ(σ − λᵢ)(2 − ‖w(k)‖²) × [2 + η((σ + λᵢ)(2 − ‖w(k)‖²) − 2wᵀ(k)Cw(k))] zᵢ²(k).

Then

σ(2 − ‖w(k)‖²) − wᵀ(k + 1)Cw(k + 1) = [σ(2 − ‖w(k)‖²) − wᵀ(k)Cw(k)]² × [(1 − ηwᵀ(k)Cw(k))² − η²σ(2 − ‖w(k)‖²)wᵀ(k)Cw(k)] + Q(k),

for k ≥ 0. Denote

V(k) = |σ(2 − ‖w(k)‖²) − wᵀ(k)Cw(k)|,

for k ≥ 0. By the invariance of S, w(k) ∈ S for k ≥ 0. It follows that,

V(k + 1) ≤ V(k) · |(1 − ηwᵀ(k)Cw(k))² − η²σ(2 − ‖w(k)‖²)wᵀ(k)Cw(k)| + |Q(k)|

≤ max{(1 − ηwᵀ(k)Cw(k))², η²σ(2 − ‖w(k)‖²)wᵀ(k)Cw(k)} · V(k) + |Q(k)|

≤ max{(1 − ηwᵀ(k)Cw(k))², ησ(2 − ‖w(k)‖²)} · V(k) + |Q(k)|.