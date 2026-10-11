make this clearer:

```
```
#!/bin/sh
fruitlist="Apple Pear Tomato Peach Grape"
for fruit in $fruitlist
do
    if [ "$fruit" = "Tomato" ] || [ "$fruit" = "Peach" ]
    then
        echo "I like ${fruit}es"
    else
        echo "I like ${fruit}s"
    fi
done
```
```

In this example, fruitlist is word, fruit is variable and the body of the statement outputs how much this person loves various fruits but includes an if... then... else statement to deal with the correct addition of letters to describe the plural version of the fruit, notice that the variable fruit was expressed like ${fruit} because otherwise the shell would have interpreted the preceding letter(s) as being part of the variable and echoed nothing because we have not defined the variables fruits and fruites When executed this script will output:

```
```
I like Apples
I like Pears
I like Tomatoes
I like Peachs
I like Grapes
```
```

Within the for construct, do and done may be replaced by ‘{’ and ‘}’.

# Case

The case construct has the following syntax:

```
```
case word in
pattern) list ;;
...

case
```
```

An example of this should make things clearer: