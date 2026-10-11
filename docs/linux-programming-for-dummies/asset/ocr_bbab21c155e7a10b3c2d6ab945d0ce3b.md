3. Modify the preceding program so that a personal greeting appears only if the user doesn't enter the name Tom and doesn't enter the word stop.

```
#!/bin/bash
declare flag="go"
while [ "$flag" -eq "go" ]
do
    clear
    echo "Enter your name or type stop to end:"
    read friend
    if [ "$friend" -eq "stop" ]
    then
        break
    fi
    if [ "$friend" -eq "Tom" ]
    then
        continue
    fi
    echo "Hello, $friend"
done
```

4. Write a program using the if statement to determine whether a last name is Smith and then determine whether the first name is Bob. If they match, say Hello to Bob Smith on-screen.

Hint: Use nested if statements.

```
#!/bin/bash
declare fname="Bob"
declare lname="Smith"
if [ "$lname" -eq "Smith" ]
then
    if [ "$fname" -eq "Bob" ]
    then
        echo "Hello Bob Smith"
    fi
fi
```

5. Write a program that displays name has these degree degrees but substituting Bob, Mary, and Joan for name and BS, MS, and Ph. D. for degree.

Hint: Use a nested for in loop.

```
#!/bin/bash
for name in Bob Mary Joan
do
    for degree in BS MS Ph.D.
    do
        echo "$name has these $degree degrees"
    done
done
```