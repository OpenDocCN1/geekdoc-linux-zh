# Chapter 13: More Structured Commands

```
for ( i = 0; i < 10; i++)
{
    printf("The next number is %d\n", i);
}
```

This code produces a simple iteration loop, where the variable i is used as a counter. The first section assigns a default value to the variable. The middle section defines the condition under which the loop will iterate. When the defined condition becomes false, the for loop stops iterations. The last section defines the iteration process. After each iteration, the expression defined in the last section is executed. In this example, the i variable is incremented by 1 after each iteration.

The Bash shell also supports a version of the for loop that looks similar to the C-style for loop, although it does have some subtle differences, including a couple of things that will confuse shell script programmers. Here's the basic format of the C-style Bash for loop:

```
for ( variable_assignment ; condition ; iteration_process )
```

The format of the C-style for loop can be confusing for Bash shell script programmers, because it uses C-style variable references instead of the shell-style variable references. Here's what a C-style for command looks like:

```
for ( a = 1; a < 10; a++ )
```

Notice that there are a couple of things that don't follow the standard Bash shell for method:

+   □ The assignment of the variable value can contain spaces.
+   □ The variable in the condition isn't preceded with a dollar sign.
+   □ The equation for the iteration process doesn't use the expr command format.

The shell developers created this format to more closely resemble the C-style for command. Although this is great for C programmers, it can throw even expert shell programmers into a tizzy. Be careful when using the C-style for loop in your scripts.

Here's an example of using the C-style for command in a Bash shell program:

```
$ cat test8
#!/bin/bash
# testing the C-style for loop

for ( i=1; i <= 10; i++ )
do
	echo "The next number is $i"
done
$ ./test8
The next number is 1
The next number is 2
The next number is 3
The next number is 4
The next number is 5
The next number is 6
The next number is 7
The next number is 8
```