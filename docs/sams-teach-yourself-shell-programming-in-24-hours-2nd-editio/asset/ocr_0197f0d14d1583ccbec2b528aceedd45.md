Using the if statement, the script is

```
#!/bin/sh
awk '{
    printf "%s\t$%s", $8;
    if ( $2 ~ /[3-9][0-9]*|[0-9][0-9]/ ) {
        printf " * ";
        if ( $3 > 75 ) {
            printf "REORDER\n";
        } else {
            printf "\n";
        }
    } else {
        if ( $3 < 75 ) {
            printf "REORDER\n";
        } else {
            printf "\n";
        }
    }
}' fruit.prices.txt ;
```

If the script is called reorder_expensive.sh and is located in the current directory, it can be invoked as follows:

```
$ ./reorder_expensive.sh
```

The output looks like the following

Fruit    Price/lbs    Quantity
Banana   $0.89        100
Peach    $0.79        65       * REORDER
Kiwi     $1.50        22       * REORDER
Pineapple $1.29       35       * REORDER
Apple    $0.99        78

# The while Statement

The while statement executes awk commands while an expression is true. The basic syntax is

```
while (expr) {
    actions
}
```