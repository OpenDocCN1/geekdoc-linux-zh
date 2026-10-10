Run the following command to do the division of the data:

```
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
```

# Training the Algorithm

We now need to train the algorithm. This can be done by calling the $fit()$ method, as we did previously. Let us first import the *LinearRegression* class from the Scikit-Learn library:

```
from sklearn.linear_model import LinearRegression
```

Next, create an instance of the above class then use it to call the $fit()$ method:

```
linear_regressor = LinearRegression()
linear_regressor.fit(X_train, y_train)
```

Note that this is a multiple linear regression and we have many variables. The linear regression model has to find the optimal coefficients for each attribute. You can see the chosen coefficients by running the following command:

```
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

# Predicting

We will make the predictions using the test data. The following script can help us do this:

```
pred_y = linear_regressor.predict(X_test)
```

At this point, you have the actual X_text values as well as the predicted values. We need to