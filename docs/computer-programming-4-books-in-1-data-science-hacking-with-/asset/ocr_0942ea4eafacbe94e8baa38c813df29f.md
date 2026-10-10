```
dataset = pd.read_csv('Market_Basket_Optimisation.csv', header = None)
```

Next is we add the items in a list so that we can work on them much easier. We can accomplish this by initializing an empty list and then running a for loop (still remember how to do all these?):

```
transactions = []
for i in range(0, 7501):
    transactions.append([str(dataset.values[i,j]) for j in range(0, 20)])
```

After we’ve done that, we should then generate a list of “related products” with their corresponding level of support or relatedness. One way to accomplish this is by the implementation of the Apriori algorithm (for association rule learning). Thankfully, we don’t have to write anything from scratch.

We can use Apypori, which is a simple implementation of the Apriori algorithm.

It’s prebuilt for us and almost ready for our own usage. It’s similar to how we use scikit-learn, Pandas, and numpy. Instead of starting from scratch, we already have blocks of code we can simply implement. Take note that coding everything from scratch is time-consuming and technically challenging. To implement Apypori, we can import it similarly as how we import other libraries:

```
from apyori import apriori
```

Next is we set up the rules (the levels of minimum relatedness) so we can somehow generate a useful list of related items. That’s because almost any two items might have some level of relatedness. The objective here is to include only the list that could be useful for us.

```
rules = apriori(transactions, min_support = 0.003, min_confidence = 0.2, min_lift = 3, min_length = 2)
```

Well that’s the implementation of Apriori using Apypori. The next step is to generate and view the results. We can accomplish this using the following block of code:

```
results = list(rules)
results_list = []
for i in range(0, len(results)):
    results_list.append('RULE:\t' + str(results[i][0][0]) + '\nSUPPORT:\t' + str(results[i][1]))
print(results_list)
```