By using `$Salary != 3000`, you're asking the computer to compare the value of the `$Salary` variable with the value `3000`. (The `!=` is a comparison operator, which I explain very soon.) If the variable has the same value, the statement is true. And in the following example, you can just assume that it's true:

```
`$Salary != 3000`
```

By using `!$Salary != 3000`, you're asking the computer to perform the same analysis, which results in a true statement. But then you tell the computer to *reverse* the value of the statement. So instead of the computer saying that the statement is true (which it is), the computer says that the statement is false because of the `!` operator.

# # The `&&` (and) operator

The `&&` (*and*) operator tells the computer to compare two variables. Each variable has either a `true` or a `false` value. Basing its conclusion on these values, the computer tells you that the statement is `true` or `false`. Here's how it works:

```
```plain
BuyCar = LowestPrice && LikeCar
```
```

The computer decides whether the **value** of the `BuyCar` variable is `true` or `false` by checking the values of the `LowestPrice` and `LikeCar` variables. The `&&` operator tells the computer to return a `true` value only if the `LowestPrice` and `LikeCar` both have a `true` value. Following are all the possible outcomes:

| BuyCar | LowestPrice | LikeCar |
| :----- | :---------- | :------ |
| True   | True        | True    |
| False  | False       | False   |
| False  | True        | False   |
| False  | False       | True    |

# # The `||` (or) operator

The `||` (*or*) operator tells the computer to compare two variables, each one having a `true` or `false` value. Basing its conclusion on these values, the computer returns either a `true` or `false` value, as in the following example:

```
```plain
BuyCar = LowestPrice || LikeCar
```
```

The computer decides whether the **value** of the `BuyCar` variable is `true` or `false` by checking the values of the `LowestPrice` and `LikeCar` variables. The