# # 1
## Introduction

# ### 1.1 Introduction

Subspace leaning neural networks provide a parallel online automated learning of low-dimensional models in a nonstationary environment. It is commonly known that automated learning of low-dimensional linear or multilinear models from training data has become a standard paradigm in computer vision [54, 55]. Thus, these neural networks used to learning a low-dimensional model have many important applications in computer vision, such as structure from motion, motion estimation, layer extraction, object recognition, and object tracking [18, 19, 50, 56, 55].

Subspace learning algorithms used to update the weights of these networks pay a vital important role in applications. This book will focus on the subspace learning algorithms of principal component analysis (PCA) neural networks, minor component analysis (MCA) neural networks, and independent component analysis (ICA) neural networks. Generally, they are linear neural networks.

# #### 1.1.1 Linear Neural Networks

Inspired by biological neural networks, a simple neural model is designed to mimic its biological counterpart, the neuron. The model accepted the weighted set of input $x$ responds with an output $y$, as shown in Figure 1.1. The vital effect of synapse between neurons is presented by the weights $w$. The mathematical model of a linear single neuron is as follows:

$$y(k)=w^T(k)x(k),\quad (k=0,1,2,\ldots), \tag{1.1}$$

where $y(k)$ is the network output, the input sequence

$$\{x(k)\mid x(k)\in R^n(k=0,1,2,\ldots)\} \tag{1.2}$$

is a zero-mean stochastic process, each $w(k)\in R^n(k=0,1,2,\ldots)$ is a weight vector.

Consider input output relation

$$y(k)=W^T x(k), \tag{1.3}$$