“greater than” or <“less than” operator is often used to test the value of an iteration counter in a loop.

Adding the = operator after a > “greater than” or < “less than” operator makes it also return **True** if the two operands are exactly equal in value.

+   1. Start a new Python script by initializing five variables with values for comparison

```
```
  nil = 0
  num = 0
  max = 1
  cap = 'A'
  low = 'a'
```
```

![](bbox=[0.11, 0.34, 0.22, 0.45])

+   2. Next, add statements to display the results of numeric and character equality comparisons

```
```
print( 'Equality \t', nil, '==', num, nil == num )
print( 'Equality \t', cap, '==', low, cap == low )
```
```

+   3. Now, add a statement to display the result of an inequality comparison

```
```
print( 'Inequality \t', nil, '!=', max, nil != max )
```
```

+   4. Then, add statements to display the results of greater and lesser comparisons

```
```
print( 'Greater \t', nil, '>', max, nil > max )
print( 'Lesser \t', nil, '<', max, nil < max )
```
```

+   5. Finally, add statements to display the results of greater or equal and lesser or equal comparisons

```
```
print( 'More Or Equal \t', nil, '>=', num, nil >= num )
print( 'Less or Equal \t', max, '<=', num, max <= num )
```
```

+   6. Save the file in your scripts directory, then open a Command Prompt window there and run this program – to see the result of comparison operations