
total transactions, the better. Or, if the percentage still falls under our arbitrary threshold (e.g., 30%, 20%), we could still pay attention to a particular set and make adjustments to our products and offers. Aside from calculating the actual percentage, another way to know how “popular” an itemset is by working on probabilities. For example, how likely is product X to appear with product Y? If there’s a high probability, we can somehow say that the two products are closely related. Those are ways of estimating the “relatedness” or level of association between two products. One or a combination of approaches might be already enough for certain applications. Perhaps working on probabilities yields better results. Or, prioritizing a very popular itemset (high percentage of occurrence) results to more transactions. In the end, it might be about testing different approaches (and combinations of products) and then seeing which one yields the optimal results. It might be even the case that a combination of two products with very low relatedness allows for more purchases to happen.

## Apriori

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

```python
import pandas as pd
```

```python
dataset = pd.read_csv('Market_Basket_Optimisation.csv', header=None)
```

Next is we add the items in a list so that we can work on them much easier. We can accomplish this by initializing an empty list and then running a for loop (still remember how to do all these?):

```python
transactions = []
for i in range(0, 7501):
    transactions.append([str(dataset.values[i, j]) for j in range(0, 20)])
```

After we’ve done that, we should then generate a list of “related products” with their corresponding level of support or relatedness. One way to accomplish this is by the implementation of the Apriori algorithm (for association rule learning). Thankfully, we don’t have to write anything from scratch.

We can use apyori, which is a simple implementation of the Apriori algorithm. It’s prebuilt for us and almost ready for our own usage. It’s similar to how we use scikit-learn, Pandas, and numpy. Instead of starting from scratch, we already have blocks of code we can simply implement. Take note that coding everything from scratch is time-consuming and technically challenging. To implement apyori, we can import it similarly as how we import other libraries:

```python
from apyori import apriori
```

Next is we set up the rules (the levels of minimum relatedness) so we can somehow generate a useful list of related items. That’s because almost any two items might have some level of relatedness. The objective here is to include only the list that could be useful for us.

```python
rules = apriori(transactions, min_support=0.003, min_confidence=0.2, min_lift=3, min_length=2)
```

Well that’s the implementation of Apriori using apyori. The next step is to generate and view the results. We can accomplish this using the following block of code:

```python
results = list(rules)
results_list = []
for i in range(0, len(results)):
    results_list.append('RULE:\t' + str(results[i][0][0]) + '\nSUPPORT:\t' + str(results[i][1]))
print(results_list)
```

When you run all the code in Jupyter Notebook, it will be messy and almost incomprehensible. But if you run it in Spyder (another useful data science package included in Anaconda installation), the result will look a bit neater: Notice that there are different itemsets with their corresponding “Support.” The higher the Support, we can somehow say that the higher the relatedness. For instance, light cream and chicken often go together because people might be using the two to cook something. Another example is in the itemset with an index of 5 (tomato sauce and ground beef). These two items might always go together in the grocery bag because they’re also used to prepare a meal or a recipe.

This is only an introduction to Association Rule Learning. The goal here was to explore the potential applications of it to real-world scenarios such as market basket optimization. There are other, more sophisticated ways to do this. But in general, it’s about determining the level of relatedness among the items and then evaluating that if it’s useful or good enough.

## Chapter 13: Reinforcement Learning

Notice that in the previous chapters, the focus is on working on past information and then deriving insights from it. In other words, we’re much focused on the past than on the present and future. But for data science and machine learning to become truly useful, the algorithms and systems should work on real-time situations. For instance, we require systems that learn real-time and adjust accordingly to maximize the rewards.

### What is Reinforcement Learning?

This is where Reinforcement Learning (RL) comes in. In a nutshell, RL is about reinforcing the correct or desired behaviors as time passes. A reward for every correct behavior and a punishment otherwise. Recently RL was implemented to beat world champions at the game of Go and successfully play various Atari video games (although Reinforcement Learning there was more sophisticated and incorporated deep learning). As the system learns from reinforcement, it was able to achieve a goal or maximize the reward.

One simple example is in the optimization of click-through rates (CTR) of online ads. Perhaps you have 10 ads that essentially say the same thing (maybe the words and designs are slightly different from one another). At first, you want to know which ad performs best and yields the highest CTR. After all, more clicks could mean more prospects and customers for your business. But if you want to maximize the CTR, why not perform the adjustments as the ads are being run? In other words, don’t wait for your entire ad budget to run out before knowing which one performed best. Instead, find out which ads are performing best while they’re being run. Make adjustments early on, so later, only the highest-performing ads will be shown to the prospects.

It’s very similar to a famous problem in probability theory about the multi-armed bandit problem. Let’s say you have a limited resource (e.g., advertising budget) and some choices (10 ad variants). How will you allocate your resource among those choices so you can maximize your gain (e.g., optimal CTR)?

First, you have to “explore” and try the ads one by one. Of course, if you’re seeing that Ad 1 performs unusually well, you’ll “exploit” it and run it for the rest of the campaign. You don’t need to waste your money on underperforming ads. Stick to the winner and continuously exploit its performance. There’s one catch, though. Early on, Ad 1 might be performing well, so we’re tempted to use it again and again. But what if Ad 2 catches up and if we let things unfold Ad 2 will produce higher gains?

We'll never know because the performance of Ad 1 was already exploited. There will always be tradeoffs in many data analysis and machine learning projects. That's why it's always recommended to set performance targets beforehand instead of wondering about the what-ifs later. Even in the most sophisticated techniques and algorithms, tradeoffs and constraints are always there.

### Comparison with Supervised & Unsupervised Learning

Notice that the definition of Reinforcement Learning doesn't exactly fit under either Supervised or Unsupervised Learning. Remember that Supervised Learning is about learning through supervision and training. On the other hand, Unsupervised Learning is actually revealing or discovering insights from unstructured data (no supervision, no labels).

One key difference compared to RL is in maximizing the set reward, learning from user interaction, and the ability to update itself in real-time. Remember that RL is first about exploring and exploiting. In contrast, both Supervised and Unsupervised Learning can be more about passively learning from historical data (not real-time). There's a fine boundary among the 3 because all of them are still concerned about optimization in one way or another. Whichever is the case, all 3 have useful applications in both scientific and business settings.

### Applying Reinforcement Learning

RL is particularly useful in many business scenarios, such as optimizing click through rates. How can we maximize the number of clicks for a headline? Take note that news stories often have limited lifespans in terms of their relevance and popularity. Given that limited resource (time), how can we immediately show the best performing headline?

This is also the case in maximizing the CTR of online ads. We have a limited ad budget, and we want to get the most out of it. Let's explore an example (using the data from Ads_CTR_Optimisation.csv) to better illustrate the idea: As usual, we first import the necessary libraries so that we can work on our data (and also for data visualization).

```python
import matplotlib.pyplot as plt
import pandas as pd
%matplotlib inline # so plots can show in our Jupyter Notebook

# We then import the dataset and take a peek
dataset = pd.read_csv('Ads_CTR_Optimisation.csv')
dataset.head(10)
```
