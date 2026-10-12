end up with the next smallest value contained in the second location of the array when the process is complete.

It should now be clear how you can go about sorting the array by performing these successive comparisons and exchanges as needed. The process stops after you have compared the next-to-last element of the array against the last and have interchanged their values if required. At that point, the entire array has been sorted into ascending order.

The following algorithm gives a more concise description of the preceding sorting process. This algorithm assumes that you are sorting an array $a$ of $n$ elements.

# Simple Exchange Sort Algorithm

+   * Step 1. Set $i$ to 0.
+   * Step 2. Set $j$ to $i + 1$.
+   * Step 3. If $a[i] > a[j]$, exchange their values.
+   * Step 4. Set $j$ to $j + 1$. If $j < n$, go to step 3.
+   * Step 5. Set $i$ to $i + 1$. If $i < n - 1$, go to step 2.
+   * Step 6. $a$ is now sorted in ascending order.

Program 7.12 implements the preceding algorithm in a function called $\mathcal{S}$ , which takes two arguments: the array to be sorted and the number of elements in the array.

# Program 7.12 Sorting an Array of Integers into Ascending Order

Click here to view code image

```
```
 /
#
{


}
i
{
```

```