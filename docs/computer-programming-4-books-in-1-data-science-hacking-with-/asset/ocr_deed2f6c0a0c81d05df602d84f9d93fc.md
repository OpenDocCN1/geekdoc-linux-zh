# **Chapter 9: How to use Scikit-Learn**

Now that you are done with the installations, you can begin to use the libraries. We will begin with the Scikit-Learn library.

To be able to use scikit-learn in your code, you should first import it by running this statement:

**import sklearn**

# **Loading Datasets**

Machine learning is all about analyzing sets of data. Before this, we should first load the dataset into our workspace. The library comes loaded with a number of datasets that we can load and work with. We will demonstrate this by using a dataset known as *Iris*. This is a dataset of flowers. The following code shows how we can use scikit-learn to load the dataset:

```
# Import scikit-learn library
from sklearn import datasets
# Load iris dataset
iris = datasets.load_iris()
# Confirm by printing the shape of the data
print(iris.data.shape)
```

# **Simple Linear Regression**

We need to use our previous example, which is, predicting the number of marks a student will score in a test depending on the number of hours they have studied for the test. It is a simple linear regression task since we only have two variables.

# **Import Libraries**

Run the following Python statements to import all the necessary libraries:

```
import numpy as np
import pandas as pd

import matplotlib.pyplot as plt
```