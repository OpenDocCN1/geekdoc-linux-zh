The idea behind the KNN algorithm is quite simple. It computes the distance of the new data point to all the other training data points. The distance can be of different types, including Euclidean, Manhattan, etc. The K-nearest data points are selected, where K can be an integer. Lastly, the data point is assigned to the class, which most of the K data points belong to.

Remember that Logistic Regression appears to feature a linear boundary between 0s and 1s. Therefore, it lacks a few of the data points that require to be on the other end. Luckily, there are non-linear models that feature a lot of data points in a more accurate style. One of them is the application of K-Nearest Neighbors. It operates by letting a new data point and then counting the number of neighbors that belong to either category. In case a lot of neighbors belong to category A than category B, then the new point should be part of category A.

Therefore, the classification of a given point depends on the majority of its nearest neighbors. This can be achieved the following line of code:

```
```python
from sklearn.neighbors import KNeighborsClassifier
classifier = KNeighborsClassifier(n_neighbors = 5, metric = 'minkowski', p = 2)
classifier.fit(X_train, y_train)
```
```

Also, rather than starting from square one, we will import the prebuilt code that simplifies our task. The behind the scenes can be learned and studied. But for many reasons, the prebuilt ones are better to make reasonably helpful models.

Don’t forget that the boundary is non-linear because of the various approach by the K-NN algorithm. Also, remember that the misses still exist. For you to capture all the misses, you need to use a larger dataset or a different method.

# The Decision Tree Classification

Many data scientists also apply decision trees in classification. Building a decision tree involves dividing a dataset into smaller subsets while separating them out. Take a look at the example below: