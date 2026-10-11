```
read y
(( sum=x+y ))
echo "The result of addition=$sum"
```

Adding numbers is very straightforward using a bash script.

# Adding Multiple Numbers

Adding multiple numbers can be a bit tricky, and you will have to use loops. Let us look at an example.

```
#!/bin/bash

sum=0

for (( counter=1; counter<5; counter++ ))
do
	echo -n "Enter Your Number:"
	read n
	(( sum+=n ))
	#echo -n "$counter "
done

printf "\n"
echo "Result is: $sum"
```

Run this script and see how many numbers this script allows you to add before printing the sum.

Linux shell scripts can be used for any task that you wish to perform on the Linux operating system. It has unlimited potential, and there is literally no limit to what you can achieve with it. We would encourage you to practice every bash script that we have provided in this chapter and even make your own changes to it to see how the output changes.