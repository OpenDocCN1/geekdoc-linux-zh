
In the training done above, we have created a linear regression model, which is the equation. The values for the slope and the intercept are known. We can make predictions based on the data we preserved as the training set. The following statement helps us make predictions from the test data:

```python
pred_y = linear_regressor.predict(X_test)
```

We have simply created a numpy array named pred_y. This will have all the predicted values for y from the input values contained in the X_test series. We now have the actual values for the X_test as well as the predicted values. We need to compare these two and see the amount of similarity or difference between the two. Just run the following code:

```python
df = pd.DataFrame({'Actual': y_test, 'Predicted': pred_y})
print(df)
```

The model is not accurate, but the values are close to each other.

## Evaluating the Accuracy

We now need to evaluate the accuracy of our algorithm. We need to determine how well the algorithm performed on the dataset. When it comes to regression algorithms, three evaluation metrics are used. These include the following:

- 1. Mean Absolute Error.
- 2. Mean Square Error.
- 3. Root Mean Squared Error.

## Multiple Linear Regression

You now know how to do a Linear Regression when you have two variables. However, this is not a true reflection of what we have in the real world. Most of the problems the world is facing involve more than two variables. This explains why you need to learn Multiple Linear Regression. The steps between the two are almost the same. However, the difference comes when it comes to evaluation. When evaluating the multiple linear regression model, we need to know the factor with the highest impact on the output variable. We also need to determine the relationship between the various variables.

We need to demonstrate this by predicting the consumption of fuel in US states. We will consider factors like per capita income, gas taxes, paved highways, and the proportion of persons who have a driver's license.
Let us first import the libraries that we need to use:

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
```

Again, you may get an error for trying to print the contents of the dataset. Use the method we used previously to solve the problem. You should have the following code:

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import sys
sys.stdout = sys.stdout
dataset = pd.read_csv('fuel_consumption.csv')
print(dataset.head())
```

### Data Preparation

In the example of simple linear regression, we subdivided the data into attributes and labels. In this case, we will be directly using the column names for this purpose. Run the code given below:

```python
X = dataset[['Tax', 'Income', 'Highways', 'Licence']]
y = dataset['Consumption']
```

We have four columns for the attributes (the independent variables) and one column for the label (the dependent variable).

Let us now subdivide the data into training and test sets. 80% of the data will be used as the training set while the remaining 20% will be used as the test set: First, let us import the train_test_split() method from Scikit-Learn:

```python
from sklearn.model_selection import train_test_split
```

Run the following command to do the division of the data:

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
```

## Training the Algorithm

We now need to train the algorithm. This can be done by calling the fit() method, as we did previously. Let us first import the LinearRegression class from the Scikit-Learn library:

```python
from sklearn.linear_model import LinearRegression
```

Next, create an instance of the above class then use it to call the fit() method:

```python
linear_regressor = LinearRegression()
linear_regressor.fit(X_train, y_train)
```

Note that this is a multiple linear regression and we have many variables. The linear regression model has to find the optimal coefficients for each attribute. You can see the chosen coefficients by running the following command:

```python
coeff = pd.DataFrame(linear_regressor.coef_, X.columns, columns=['Coefficient'])
print(coeff)
```

| | Coefficient |
|---|---|
| Tax | -40.016660 |
| Income | -0.065413 |
| Highways | -0.004741 |
| Licence | 1341.862121 |

This means that any unit increase in fuel tax will lead to a decrease of 40.02 million gallons in gas Consumption. Also, a unit increase in the proportion of the population with Driver’s license will lead to an increase of 1.342 billion gallons in gas Consumption. The results also show that average Income and Highways have a very small impact on gas Consumption.

## Predicting

We will make the predictions using the test data. The following script can help us do this:

```python
pred_y = linear_regressor.predict(X_test)
```

At this point, you have the actual X_test values as well as the predicted values. We need to perform a comparison between these two to determine their similarities and differences. This can be done by running the following script:

```python
df = pd.DataFrame({'Actual': y_test, 'Predicted': pred_y})
print(df)
```

## Evaluating the Accuracy

We now need to evaluate the algorithm in terms of performance. This can be done by determining the values for the various types of errors. These include the MAE, RMSE, and MSE. This requires us to import the metrics class from Scikit-Learn:

```python
from sklearn import metrics
```

The calculation of the error values can then be done using the following script:

```python
print('MAE:', metrics.mean_absolute_error(y_test, pred_y))
print('MSE:', metrics.mean_squared_error(y_test, pred_y))
print('RMSE:', np.sqrt(metrics.mean_squared_error(y_test, pred_y)))
```

The value for the root mean square error is 68.31, as shown above. This is slightly greater than 10% of the mean value for gas consumption in all the states. It is true that our algorithm was not very much accurate, but we can still use it to make predictions. The big error could be brought by a number of factors. Maybe there was a need for more data. We have used data for only one year. Having data collected over multiple years could have helped us improve the accuracy of the model. Also, we had assumed that our data has a linear relationship. This could not be the case, hence the big error. I recommend that you visualize the data to see whether this is true. Also, the features we have used could not be correlated.

# Chapter 10: K-Nearest Neighbors Algorithm

The KNN algorithm is highly used for building more complex classifiers. It is a simple algorithm, but it has outperformed many powerful classifiers. That is why it is used in numerous applications data compression, economic forecasting, and genetics. KNN is a supervised learning algorithm, which means that we are given a labeled dataset made up of training observations (x, y) and our goal is to determine the relationship between x and y. This means that we should find a function that x to y such that when we are given an input value for x, we are able to predict the corresponding value for y. The concept behind the KNN algorithm is very simple. We will use a dataset named Iris. We had explored it previously. We will be using this to demonstrate how to implement the KNN algorithm.

First, import all the libraries that are needed:

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
```

## Splitting the Dataset

We need to be able to tell how well our algorithm performed. This will be done during the testing phase. This means that we should have training and testing data. The data set should be divided into two parts. We need to split the data into two parts. 80% of the data will be used as the training set, while 20% will be used as the test set. Let us first import the train_test_split method from Scikit-Learn.

## Feature Scaling

Before we can make real predictions, it is a good idea for us to scale the features. After that, all the features will be evaluated uniformly. Scikit-Learn comes with a class named StandardScaler, which can help us perform the feature scaling. Let us first import this class.

We then instantiate the class then use it to fit a model based on it:
