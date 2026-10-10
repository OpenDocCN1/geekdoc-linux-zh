```
```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
```
```

Again, you may get an error for trying to print the contents of the dataset. Use the method we used previously to solve the problem. You should have the following code:

```
```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import sys
sys.stdout = sys.stdout
dataset = pd.read_csv('fuel_consumption.csv')
print(dataset.head())
```
```

# ### Data Preparation

In the example of simple linear regression, we subdivided the data into attributes and labels. In this case, we will be directly using the column names for this purpose. Run the code given below:

```
```python
X = dataset[['Tax', 'Income', 'Highways',
'Licence']]
y = dataset['Consumption']
```
```

We have four columns for the attributes (the independent variables) and one column for the label (the dependent variable).

Let us now subdivide the data into training and test sets. 80% of the data will be used as the training set while the remaining 20% will be used as the test set:
First, let us import the *train_test_split()* method from Scikit-Learn:

**from sklearn.model_selection import train_test_split**