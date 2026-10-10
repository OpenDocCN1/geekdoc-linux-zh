total transactions, the better. Or, if the percentage still falls under our arbitrary threshold (e.g., 30%, 20%), we could still pay attention to a particular set and make adjustments to our products and offers. Aside from calculating the actual percentage, another way to know how “popular” an itemset is by working on probabilities. For example, how likely is product X to appear with product Y? If there’s a high probability, we can somehow say that the two products are closely related. Those are ways of estimating the “relatedness” or level of association between two products. One or a combination of approaches might be already enough for certain applications. Perhaps working on probabilities yields better results. Or, prioritizing a very popular itemset (high percentage of occurrence) results to more transactions. In the end, it might be about testing different approaches (and combinations of products) and then seeing which one yields the optimal results. It might be even the case that a combination of two products with very low relatedness allows for more purchases to happen.

# Apriori

Whichever is the case, let’s explore how it all applies to the real world. Let’s call the problem “Market Basket Optimization.” Our goal here is to generate a list of sets (product sets) and their corresponding level of relatedness or support to one another. Here’s a peek of the dataset to give you a better idea:

```
shrimp,almonds,avocado,vegetables mix,green grapes,whole wheat flour,yams,cottage cheese,energy drink,tomato juice,low fat yogurt,green tea,honey,salad,mineral water,salmon,antioxidant juice,frozen smoothie,spinach,olive oil
burgers,meatballs,eggs
chutney
turkey,avocado
mineral water,milk,energy bar,whole wheat rice,green tea
low-fat yogurt
whole-wheat pasta,french fries
soup,light cream,shallot
frozen vegetables,spaghetti,green tea
french fries
```

Those are listed according to the transactions where they appear. For example, in the first transaction, the customer bought different things (from shrimp to olive oil). In the second transaction, the customer bought burgers, meatballs, and eggs.

As before, let’s import the necessary library/libraries so that we can work on the data:

```
import Pandas as pd
```