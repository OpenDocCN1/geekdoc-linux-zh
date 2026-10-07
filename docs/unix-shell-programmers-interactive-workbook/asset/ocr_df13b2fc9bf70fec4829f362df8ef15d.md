# Consider the following script:

```
# s713 -- Tell if the user typed the name of a month
grep "^$1$\$ Months > /dev/null || print -- "$1 is not
the name of a month.
```

a) Explain how this script works.

# 7.1.4 NEST if STATEMENTS

You can put one if statement "inside" another one, which is known as nesting.
The result can get confusing, but simple nesting can be fairly clear to follow.

Be sure you still have the days file from Exercise 3.1.3,"Pipelines" (or create it again), and run the following script:

```
# s714 -- Demonstrate nested if statements
if grep -i "^$1$\$ Months > /dev/null
ththen print -- "$1 is the name of a month.
else if grep -i "^$1$\$ days > /dev/null
	then print -- "$1 is the name of a day.
	else print -- ""\$1\" is neither a month nor a day.
fi
```

a) What happens if you give the name of a month as a parameter?

b) What happens if you give the name of a day of the week?