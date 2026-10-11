# **EXERCISE 11**
**I Can't Seem To Function Without Subroutines**

+   1. Write a program called *tripper* that will ask the user the number of miles he has driven and the amount of gas he used.
+       a. In the *tripper* script, write a subroutine called *mileage* that will calculate and return the user's mileage (miles per gallon). The number of miles driven and the amount of gas used will be passed as arguments. All variables should be *my* variables. The program should test to make sure the user doesn't enter 0 for the amount of gas. (Division by zero is illegal.)
+       b. Print the results.
+       c. Prototype *tripper*.

+   2. Hotels are often rated using stars to represent their score. A five-star hotel may have a king-size bed, a kitchen, and two TVs; a one-star hotel may have cockroaches and a leaky roof.
+       a. Write a subroutine called *prinstar* that will produce a histogram to show the star rating for hotels shown in the following hash. The *prinstar* function will be given two parameters: the name of the hotel and the number of its star rating. (Hint: sort the hash keys into an array. Use a loop to iterate through the keys, calling the *prinstar* function for each iteration.)

```
```perl
%hotels=("Pillowmint Lodge"   => "5",
        "Buxton Suites"   => "5",
        "The Middletonian"   => "3",
        "Notchbelow"   => "4",
        "Rancho El Cheapo"   => "1",
        "Pile Inn"   => "2",
        );
```
```

(OUTPUT)

| Hotel | Category |
| :--- | :--- |
| Notchbelow | **** |
| The Middletonian | *** |
| Pillowmint Lodge | ***** |
| Pile Inn | * |
| Rancho El Cheapo | * |
| Buxton Suites | ***** |