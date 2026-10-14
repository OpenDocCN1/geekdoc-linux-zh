```
#!/usr/bin/env bash
# File: simpleifelse.sh
echo "Start program"
if [[ $1 -eq 4 ]]
then
    echo "Thanks for entering $1"
else
    echo "You entered: $1, not what I was looking f\
 or ."
fi
echo "End program"
```

Now let’s try running this program a few different ways:

```
bash simpleifelse.sh 4
```

```
## Start program
## Thanks for entering 4
## End program
```

The conditional expression [[ $1 -eq 4 ]] was true so code inside of the IF statement was run and the code in the ELSE statement was not run. What do you think will happened when we make the conditional expression false?

```
bash simpleifelse.sh 3
```