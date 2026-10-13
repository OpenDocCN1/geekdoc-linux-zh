# **Definition 1.3** *a subspace is called a principal subspace if the subspace is spanned by the first few principal component directions.*

Generally, PCA has two steps. First, principal component directions must be found. In these directions, the input data have the largest variances, as shown in Figure 1.3. Then, principal components are obtained by projecting the input data into the principal directions. The principal components are uncorrelated and ordered so that the first few retain most of the variation present in all of the original data set.

PCA has a wide variety of different applications, as well as a number of different derivations [17, 24, 29, 93, 150], such as Kernel PCA [42, 99], Probabilistic PCA [170, 171, 207], Local PCA [116, 179], Generalized PCA [173], L1-PCA [104], Blockwise PCA [41, 133], Sparse PCA [208], Topological PCA [148], and Bayesian PCA [176, 112].

![](bbox=[0.294, 0.359, 0.696, 0.575])

**FIGURE 1.3**  
Principal component direction and minor component direction in a two-dimensional data set.

Traditionally, some classical methods such as QR decomposition or SVD algorithm are used to find the principal component directions. These methods are not practical to handle large data sets because of huge covariance matrix [73, 179, 189]. PCA learning algorithms offer an advantage that they can adapt online to the data and no explicit computation of the covariance matrix.

PCA learning algorithms are used to update the weights of linear neural networks so that the weights converge to the principal component directions that span a principal subspace. Then, these networks can be used to extract the principal components without calculating the covariance matrix in advanced. PCA neural networks have many applications, including applications relating to feature extraction [152, 158], fault detection [90, 109], face classification [114, 166], gender recognition [53], image compression [51], text classification [113], forecasting [118], and protein structure analysis [64].