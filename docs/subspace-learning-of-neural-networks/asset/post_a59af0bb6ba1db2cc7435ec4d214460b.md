
precision $\alpha$ by

$$m=\min\left\{Z\in\{0,1,\ldots,n\}\mid\sum_{p=1}^{Z}\lambda_p\geq\alpha\cdot\operatorname{trace}(C)\right\}, \qquad (8.1)$$

where $C\in\mathbb{R}^{n\times n}$ is the covariance matrix of the given data set, $\lambda_p$ ($p=1,\ldots,n$) are eigenvalues of $C$ with $\lambda_1\geq\lambda_2\geq\ldots\geq\lambda_n\geq 0$. The quotient between $\lambda_i$ and the trace of $C$ is the amount of variance explained by the $i$th principal direction of $C$. Hence, $\alpha$ represents the amount of variance explained by the principal directions associated with the first $m$ eigenvalues.

Although the intrinsic dimensionality $m$ is just an appropriate number of principal directions for PCA neural networks, it is not easy to compute the number $m$ in advance for online applications. In this chapter, a PCA model is proposed that is motivated by a key characteristic of biological neural networks: that excited neurons can activate neurons close to them and inhibit neurons far away from them. Using this well-known *on-center/off-surround* principle [75, 101], the proposed model together with an improved GHA algorithm is able to adapt itself. In this learning procedure, the number of active neurons, which is the same as the number of principal directions in the model, approximates the intrinsic dimensionality $m$ of the given data set to achieve the precision $\alpha$. Therefore, a good balance between the quality of computational results and the complexity of the computations of PCA neural networks can be obtained.

This chapter⁴ is organized as follows. In Section 2, the biologically plausible PCA model and the improved GHA algorithm are given. Some important properties of the model are analyzed in Section 3. Simulations are carried out in Section 4. Conclusions are drawn in Section 5.

## 8.2 The PCA Model and Algorithm

### 8.2.1 The PCA Model

Suppose an input sequence

$$\{x(k)\mid x(k)\in\mathbb{R}^{n},\ (k=1,2,\ldots)\}$$

is a zero mean stationary stochastic process. Denote $C=E[x(k)x^T(k)]$, the covariance matrix of the input data set. In 1989, Sanger [156] proposed the GHA to adaptively extract the principal components from the data set. Let $y(k)=W(k)x(k)$, where $W^T(k)=[w_1(k),w_2(k),\ldots,w_{m'}(k)]$ is the weight matrix and $y(k)=[y_1(k),y_2(k),\ldots,y_{m'}(k)]^T$ is the output vector. The GHA PCA model is presented in Figure 8.1 (left) and the GHA learning algorithm is as follows:

![](img/5d1bf22d32ba379cbf31221a5347fdb6_193_0.png)

**FIGURE 8.1**  
The original GHA model (left) and an improved GHA model with lateral connections (right).

$$W(k+1)=W(k)+\eta\left[W(k)C_k-\operatorname{LT}\left[W^T(k)C_kW(k)\right]W(k)\right]. \tag{8.2}$$

for $\eta > 0$ and $k \geq 1$, where $C_k = x(k)x^T(k)$. The operator $\operatorname{LT}[\cdot]$ sets all the elements above the diagonal of its matrix argument to zero. By (8.2), $W^T(k) = [w_1(k), w_2(k), \ldots, w_{m'}(k)]$ will converge to the principal directions of the input data set. Here, $m' \ll n$ is the number of extracted principal directions of the given data set and the number of neurons in this network. Clearly, the number $m'$ must be determined in advance to use the PCA neural network. This requirement is not practical in applications, especially for online ones.

In this chapter, an improved PCA model is proposed as shown in Figure 8.1 (right). In this model, the number of the extracted principal directions will be determined to adaptively approximate the intrinsic dimensionality of the given data set to reach a required precision. The neurons in this model are arranged in a line with lateral connections. The lateral connections serve as passages through which the output of neurons can be transmitted to other neurons so that the activation and inhibition can occur. There are two classes of neurons in this model: active neurons and resting neurons. All active neurons always line up in front of this model, and the first neuron is always at the center of all active ones. After the active neurons are excited by input with a certain magnitude, either the first resting neuron will be activated or the last active neuron will be inhibited, based on the on-center/off-surround biological perspective [75, 101]. The number of active neurons, which is just the number of the principal directions for this PCA model, approximates the intrinsic dimensionality of the data set via the biological procedure.

With the online observation $C_k$ (1.10), clearly, $\lim_{k\to\infty} C_k = C$ with $C_0 = 0$. The improved model can be presented mathematically as $y(k)=W(k)x(k)$, $(k\ge 1)$, where $W^T(k)=[w_1(k), w_2(k), \ldots, w_n(k)]$ is the weight matrix and $y(k)=[y_1(k), y_2(k), \ldots, y_n(k)]^T$ is the output vector. To update the net weights, an improved GHA learning algorithm is given by

$$W(k+1)=W(k)+\eta\Pi(k)\left[W(k)C_k-\operatorname{LT}\left[W^T(k)C_kW(k)\right]W(k)\right], \tag{8.3}$$

for $\eta > 0$ and $k \geq 1$, where $\Pi(k)$ is a diagonal matrix. $\Pi(k)$ serves as a controller at time instance $k$, which determines whether a neuron is active or resting. The values of the diagonal elements of $\Pi(k)$ are always 1 or 0, and the 1s always appear along the diagonal. If the value of a diagonal element is 1, the corresponding neuron is active. Otherwise, the neuron is resting. The initial values of all elements of $\Pi(1)$ are 0, except $\Pi_{11}(1)=1$, that is, only the first neuron is active at the initial time. It is just $\Pi(k)$, which determines the number of the extracted principal directions for the improved PCA model at time instance $k$.

The key difference between the original GHA (8.2) and the improved GHA (8.3) is that $\Pi(k)$ is added in the improved GHA. By changing the value of diagonal elements of $\Pi(k)$, the algorithm (8.3) will adaptively converge to the first $m$ principal directions of the input data set, that is, $W^T=[w_1, w_2, \ldots, w_m]$, so that the dimensionality of the data set can be reduced to the $m$-dimensional subspace online with precision $\alpha$. Here, an important problem to address is how to change the value of diagonal elements of $\Pi(k)$ so that the number of principal directions for the PCA model approximates the intrinsic dimensionality of the input data set in an online manner. The following subsection will discuss this problem.

### 8.2.2 Algorithm Implementation

The value of diagonal elements of $\Pi(k)$ is adaptively adjusted with time for the number of the extracted principal directions to approximate the intrinsic dimensionality of the input data set. The changes to the value of diagonal elements of $\Pi(k)$ effectively implement the on-center/off-surround procedure. In this section, the implementation of the algorithm will be described.

First, define two functions as follows:

$$\sigma(x)=\begin{cases}1,&\text{if }x\ge 0\\0,&\text{otherwise}\end{cases}\qquad \bar{\sigma}(x)=\begin{cases}1,&\text{if }x\ge 0\\-1,&\text{otherwise}\end{cases}$$

Denote $l(k)$ as the number of active neurons at time instance $k$, which is just the number of the extracted principal directions for the proposed PCA model. $l(k)$ is also the number of 1s in diagonal elements of $\Pi(k)$, with $l(1)=1$.

In Chapter 4, it has been proved that $w_i(k)$ converges to the $i$th principal direction of $C_k$ with $k\to\infty$, and $y_i^2(k)=w_i^T(k)C_kw_i(k)$ converges to $\lambda_i$. Thus, $\frac{\sum_{i=1}^{l(k)}y_i^2(k)}{\operatorname{tr}(C_k)}$ approximates the amount of variance expressed by the first $l(k)$ principal directions of $C_k$. Suppose the number $l(k)$ of active neurons approximates the intrinsic dimensionality of a given data set as $k\to\infty$. $f_1(k)$ represents the threshold of intrinsic dimensionality of the data set at time instance $k$ according to Rubio’s method [151]. At time instance $k$, if the amount of variance expressed by the first $l(k)$ principal directions of $C_k$ does not reach the required precision, that is, $\alpha \cdot \operatorname{trace}(C_k) > \sum_{i=1}^{l(k)} y_i^2(k)$, then $f_1(k)=1$. In this case, the first resting neuron, which is close to active neurons, may be activated. Otherwise, $f_1(k)=-1$, in which case the last active neuron may be inhibited.

$$f_1(k)=\bar{\sigma}\left[\alpha \cdot \operatorname{trace}(C_k)-\sum_{i=1}^{l(k)}y_i^2(k)\right]. \tag{8.4}$$

for $k \ge 1$, where $\alpha$ is the approximated precision and $\operatorname{trace}(C_k)$ denotes the trace of matrix $C_k$.

Clearly, the number of active neurons cannot increase indefinitely and cannot also decrease to 0. Here, $f_2(k)$ serves as the threshold of neighborhood. Let $n-l(k)$ be the maximum length of neighborhood to which the neuron may be activated. The threshold of the neighborhood is defined as

$$f_2(k)=\sigma\left(\sigma(n-l(k)-1)-f_1(k)\right). \tag{8.5}$$

for all $k\ge 1$. If and only if $f_2(k)=1$, a neuron may be activated. Clearly, $f_1(k)$ and $f_2(k)$ will jointly serve as the switch of the neighborhood.

If only $f_1(k)$ is used as an activation or inhibition condition, the number $l(k)$ of active neurons will oscillate around the intrinsic dimensionality of the input data set. This will be illustrated in Section 5. To overcome this problem, the function $f_3(k)$ is defined as follows:

$$f_3(k)=\sigma\left\{\sigma\left[\sum_{i=1}^{l(k)-1}y_i^2(k)-\alpha\cdot \operatorname{trace}(C_k)\right]+f_2(k)\right\}. \tag{8.6}$$

for all $k\ge 1$. From (8.4) and (8.6), clearly, if $\sum_{i=1}^{l(k)}y_i^2(k) > \alpha \cdot \operatorname{trace}(C_k)$ and $\sum_{i=1}^{l(k)-1}y_i^2(k) < \alpha \cdot \operatorname{trace}(C_k)$, then $f_3(k)=0$ and $f_1(k)=-1$. In this case, activation or inhibition will not take place anymore. It just serves to fulfill a stop criterion. If $\sum_{i=1}^{l(k)-1}y_i^2(k) > \alpha \cdot \operatorname{trace}(C_k)$, then $f_3(k)=1$ and $f_1(k)=-1$, in which case the last active neuron may be inhibited at the time instance $k$.
