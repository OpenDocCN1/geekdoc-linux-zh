```
then
	echo "One condition is true, this line is printed"
else
	echo "You are out of luck!"
fi

kali@kali:~$ chmod +x ./or.sh

kali@kali:~$ ./or.sh
One condition is true, this line is printed

kali@kali:~$ echo $USER && echo $HOSTNAME
kali
kali
```

*Listing 156 - Using the or (||) boolean operator to test multiple conditions in Bash*

In this example, we used **OR (||)** to test multiple conditions and since one of the variable comparisons was true, the whole *if* line succeeded, so the *then* branch executed.

# ## 5.5 Loops

In computer programming, *loops*¹¹⁹ help us with repetitive tasks that we need to run until a certain criteria is met. Iteration is particularly useful for penetration testers, so we recommend paying very close attention to this section.

In Bash, the two most predominant loop commands are *for*¹²⁰ and *while*.¹²¹ We will take a look at both.

# ### 5.5.1 For Loops

*For* loops are very practical and work very well in Bash one-liners.¹²² This type of loop is used to perform a given set of commands for each of the items in a list. Let’s briefly look at its general syntax:

```
```
for var-name in <list>
do
	<action to perform>
done
```
```

*Listing 157 - General syntax of the for loop*

The *for* loop will take each item in the *list* (in order), assign that item as the value of the variable *var-name*, perform the given action between *do* and *done*, and then go back to the top, grab the next item in the list, and repeat the steps until the list is exhausted.