**Answer:** This code actually contains two problems. The second if statement never runs because the condition requires that the `$name` not be Tom — the `if statement`, however, nests inside another `if` statement that executes only if the `$name` is Tom. The second `if` statement is missing the `fi` keyword.

4. What’s the problem with the following code? (Are you noticing a pattern with the questions for this set of exercises?)

```
#!/bin/bash
clear
case $city in
	"q")
		echo "Search by name"
		;;
	"b")
		echo "Search by telephone number"
		;;
	"c")
		echo "Search by employee number"
		;;
	"q")
		declare flag="Q"
		;;
	*)
		echo "Incorrect menu selection."
		;
	esac
```

**Answer:** You’re assigning no value to `$city`. And the `case` statement requires the `esac` keyword, which is missing from the last line of this program.

5. What’s the problem with the following code?

```
#!/bin/bash
clear
for friend in Bob Smith Mary Jones Joan Adams
do
	echo "Hi, $friend"
done
```

**Answer:** You need to enclose the names Bob Smith, Mary Jones, and Joan Adams within quotation marks:

```
for friend in "Bob Smith" "Mary Jones" "Joan Adams"
```