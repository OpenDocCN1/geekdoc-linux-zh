|0|one|1|
|3|two|3|
|4|two|3|
|5|two|4|

Here, we removed duplicates based on matching row values across all columns. Alternatively, we can also remove duplicates based on a particular column. Let’s remove duplicate values from the k1 column.

```
`data.drop_duplicated(subset='k1')`
```

|K1|K2|
|o|one|3|
|3|two|3|

Now, we will learn to categorize rows based on a predefined criterion. It happens a lot while data processing where you need to categorize a variable. For example, say we have got a column with country names, and we want to create a new variable 'continent' based on these country names.

In this case, we will follow these steps:

```
```
data = pd.DataFrame({'food': ['bacon', 'pulled pork', 'bacon',
                    'Pastrami', 'corned beef', 'Bacon', 'pastrami', 'honey ham', 'nova lox'],
                     'ounces': [4, 3, 12, 6, 7.5, 8, 3, 5, 6]})
data
```
```

Now, we want to create a new variable that indicates the type of animal which acts as the source of the food. To do that, first, we'll create a dictionary to map the food to the animals. Then, we'll use map function to map the dictionary's values to the keys. Let’s see how is it done.