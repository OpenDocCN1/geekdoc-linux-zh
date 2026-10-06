# Advanced Bash–Scripting Guide

Rows=5
Columns=5

```
declare -a alpha      # char alpha [Rows] [Columns];
                      # Unnecessary declaration.

load_alpha ()
{
    local rc=0
    local index
}

for i A B C D E F G H I J K L M N O P Q R S T U W X Y
do
    local row=$(expr rc / $Columns)
    local column=$(expr rc % $Columns)
    let "index" = $row * $Columns + $column
    alpha[$index]=$i      # alpha[$row]
    let rc += 1
done

# Simpler would be
#     declare -a alpha={A B C D E F G H I J K L M N O P Q R S T U V W X Y}
# but this simpler lacks the "flavor" of a two-dimensional array.
```

```
print_alpha ()
{
    local row=0
    local index
}

echo

while [ "$row" -lt "$Rows" ];
do
    # Print out in "row order"
    # columns vary
    # while row (outer loop) remains the same
    local column=0
    while [ "$column" -lt "$Columns" ];
do
        let index=$(expr $row * $Rows + $column)
        echo -n "${alpha[$index]}"  # alpha[$row][$column]
        let "column += 1"
    done
    let "row += 1"
done
\cho
```

> # The simpler equivalent is
# echo $${alpha[*]} | kargs -n $Columns

```
filter ()
{
    echo -n ""      # Filter negative array indices.
    #               Provides the tilt.
}

if [[ "$1" -ge 0 && "$1" -lt "$Rows" && "$2" -ge 0 && "$2" -lt "$Columns" ]];
```

Chapter 26. Arrays

283