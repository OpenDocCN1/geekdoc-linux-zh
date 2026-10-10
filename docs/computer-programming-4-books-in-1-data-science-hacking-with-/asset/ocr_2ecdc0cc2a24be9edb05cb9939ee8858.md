![](bbox=[0.07, 0.09, 0.69, 0.45])

# **Transformation of Feature**

Pandas does have different functions that can be applied in feature transformations.

For instance, the most popular machine learning libraries expect data to be in numerical form. As a result, it is important to change any non-numeric properties. The right way to achieve this is by hot encoding. Pandas have a function for this known as the get_dummies. Once this method is applied to a data column, it changes every unique value into a new binary column.

Another style which a feature may require to be converted for machine learning is called binning. A great example of this data set is the age feature. It can be significant to gather the ages into ranges for the model to learn. Pandas do have a function pd.cut that can be applied.

```
```
bins = [0, 30, 40, 50, 60, 70, 100]
train['age_group'] = pd.cut(train['age'], bins)
train['age_group'].value_counts().plot(kind='bar')
```
```