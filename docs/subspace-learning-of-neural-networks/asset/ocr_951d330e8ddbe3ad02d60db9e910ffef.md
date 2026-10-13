many fields involving signal processing [66], prediction [80], associative memory [167], function approximation [180], power system [15, 153], chemistry [196], and so on. The weight of these neural networks, which represents the strength of the connection between neurons, pays a very important role in the different applications. A variety of learning algorithms are used to update the weight so that the networks have the different applications with the corresponding weight. For instance, the adaptive linear neuron (ADALINE) network is one of the most widely used neural networks in practical applications, which was introduced by Widrow and M. Hoff in 1960 [181]. The least mean square (LMS) algorithm is used to update the weight so that ADALINE can be used as a adaptive filter [75].

In this book, these linear networks are used to extract the principal components, or minor components, or independent components from input data. It is required that these networks must approximate a low-dimensional model.

# 1.1.2  Subspace Learning Algorithms

Subspace learning algorithms are used to update the weights of these linear networks so that these networks intend to approximate a low-dimensional linear model. Generally, an original stochastic discrete time (SDT) algorithm is formulated as

$$w(k+1)=w(k)+\eta(k)\,\Delta w(k), \tag{1.4}$$

where $\eta(k)$ is learning rate and $\Delta w(k)$ determines the change at time $k$.

This book will mainly discuss the following subspace learning algorithms: PCA learning algorithms, MCA learning algorithms, and ICA learning algorithms.

# 1.1.2.1  PCA Learning Algorithms

Principal component analysis (PCA) is a traditional statistical technique in multivariate analysis, stemming from the early work of Pearson [141]. It is closely related to Karhunen-Loève (KL) transform, or the Hotelling transform [82]. The purpose of PCA is to reduce the dimensionality of a given data set, while retaining as much as possible of the information present in the data set.

**Definition 1.1**  *A vector is called the first principal component direction if the vector is along the eigenvector associated with the largest eigenvalue of the covariance matrix of a given data set, and a vector is called the second principal component direction if the vector is along the eigenvector associated with the second largest eigenvalue of the covariance matrix of a given data set, and so on.*

**Definition 1.2**  *Principal components are the variances that are obtained by projecting the given data onto the principal component directions.*