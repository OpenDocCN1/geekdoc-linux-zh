
## The while Command

I am planning to continue my travel circle across the United States in the summer. The next state I will visit is Alabama

I am planning to continue my travel circle across the United States in the summer. The next state I will visit is Texas

And so on until the last line:

I am planning to continue my travel circle across the United States in the summer. The next state I will visit is Georgia

Each time the for command iterates through the list of objects, it assigns the mytest variable to the next item in the list. The $mytest variable is used like other script variables in the for command statements. After the final iteration, the $test variable remains valid throughout the shell script's remaining part. It will retain the final iteration value unless you change it.

```bash
v=$ cat testing111
#!/bin/bash
# This is the basic for command in Linux
```

```bash
for mytest in Alabama Texas Alaska Virginia Arizona Ohio Arkansas South Dakota California North Dakota Colorado New Jersey Florida Michigan Georgia
do
    echo "I am planning to continue my travel circle across the United States in the summer. The next state I will visit is $mytest"
done
echo "The last US state I traveled to was $mytest"
mytest=Connecticut
echo "Now I am going to visit $mytest"
```

```bash
$ bash -f main.sh
```

I am planning to continue my travel circle across the United States in the summer. The next state I will visit is Alabama

I am planning to continue my travel circle across the United States in the summer. The next state I will visit is Texas

And so on, until the last line:

I am planning to continue my travel circle across the United States in the summer. The next state I will visit is Georgia

The last US state I traveled to was Georgia

Now I am going to visit Connecticut

You can see that the $mytest variable retained its original value and permitted us to change it outside the for loop. Let’s see another for loop example:

```bash
v=$ cat testing111
#!/bin/bash
# This is the basic for command in Linux
for mytest in pumpkin potato tomato spinach ginger garlic cauliflower cabbage pepper beet ladyfinger broccoli
do
    echo "I am planning to make a shift to the cooking schedule as the summer sets in. I have bought lots of vegetables. However, today I plan to cook $mytest."
done
echo "The last vegetable I cooked was $mytest"
mytest=onion
echo "Now I am going to cook $mytest"
```

```bash
$ bash -f main.sh
```

I am planning to make a shift to the cooking schedule as the summer sets in. I have bought lots of vegetables. However, today I plan to cook pumpkin.

I am planning to make a shift to the cooking schedule as the summer sets in. I have bought lots of vegetables. However, today I plan to cook potato.

This continues through each of the vegetables, ending with:

I am planning to make a shift to the cooking schedule as the summer sets in. I have bought lots of vegetables. However, today I plan to cook broccoli.

The last vegetable I cooked was broccoli

Now I am going to cook onion

When you are dealing with the for command, the biggest problem you may encounter is using multi-word values. The for loop assumes that each value ought to be separated by a space. If you have data values to contain spaces, you may run into another problem. You may see that in the example of US states. The bash editor considered South and Dakota as two separate values.

The for command offers us the quotation marks to separate values that have more than one word. You may use double quotes to separate different values in the for command. See the following example.

```bash
v=$ cat testing111
#!/bin/bash
# This is the basic for command in Linux
```

```bash
for mytest in Alabama Texas "New York" Alaska Virginia Arizona Ohio Arkansas "South Dakota" California "North Dakota" Colorado "New Jersey" Florida Michigan Georgia "North Carolina" "South Carolina" "New Mexico" "Rhode Island" "West Virginia" "New Hampshire" Vermont
do
    echo "I am planning to continue my travel circle across the United States in the summer. The next state I will visit is $mytest"
done
echo "The last US state I traveled to was $mytest"
mytest=Connecticut
echo "Now I am going to visit $mytest"
```

```bash
$ bash -f main.sh
```

I am planning to continue my travel circle across the United States in the summer. The next state I will visit is Alabama.

I am planning to continue my travel circle across the United States in the summer. The next state I will visit is Texas.

Continuing through the States until we get to the last one:

I am planning to continue my travel circle across the United States in the summer. The next state I will visit is Vermont

The last US state I traveled to was Vermont

Now I am going to visit Connecticut

Now the for command can distinguish between the single word and multi-word values. Also, the best thing is that when you are using double quotation marks, the shell sheds the quotation marks as a part of the value.

## Reading a List through a Variable

Often what happens inside a shell script is that you accumulate lists of values that are stored inside a variable. Then it needs to iterate through a list. You may do this with the help of the for command.

```bash
$ cat testing111
#!/bin/bash
# This is the basic for command in Linux

list="Alabama Texas New York Alaska Virginia Arizona Ohio Arkansas
South Dakota California North Dakota Colorado New Jersey Florida
Michigan Georgia North Carolina South Carolina New Mexico Rhode Island
West Virginia New Hampshire Vermont"

list="$list" Idaho"
for state in $list
do
    echo "I am planning to continue my travel circle across the United States in the summer. The next state I will visit is $state"
done
```

```bash
$ bash -f main.sh
```

I am planning to continue my travel circle across the United States in the summer. The next state I will visit is Alabama

I am planning to continue my travel circle across the United States in the summer. The next state I will visit is Texas

Right up to the last state:

I am planning to continue my travel circle across the United States in the summer. The next state I will visit is Idaho

The $list variable contains the list of values that have been used for iterations. You should take note that the code uses another assignment statement for the concatenation of items to the existing list. Even when you forget to add items in the list, you can add them up by the concatenation method later on. I will add five more items to the list in the next example.

```bash
$ cat testing111
#!/bin/bash
# This is the basic for command in Linux
list="Alabama Texas Alaska Virginia Arizona Ohio Arkansas California Colorado Florida
Michigan Georgia Vermont Iowa Nebraska Arkansas Kansas Kentucky Tennessee Utah
Maine Missouri Minnesota"
list=$list" Idaho"
list=$list" Oregon"
list=$list" Montana"
list=$list" Delaware"

for state in $list
do
    echo "I am planning to continue my travel circle across the United States in the summer. The next state I will visit is $state"
done
```

```bash
$ bash -f main.sh
```

I am planning to continue my travel circle across the United States in the summer. The next state I will visit is Alabama

I am planning to continue my travel circle across the United States in the summer. The next state I will visit is Texas

This output continues to list the states, right up to the last one:

I am planning to continue my travel circle across the United States in the summer. The next state I will visit is Delaware

There is a way to generate values for custom usage in a list to use the output of a particular command.

```bash
$ cat testing111
#!/bin/bash
# I will read values from files
myfile="states"
```

```bash
for state in `cat $myfile`
do
    echo "I am planning to continue my travel circle across the United States in the summer. The next state I will visit is $state"
done
```

```
Alabama
Alaska
Arizona
Arkansas
California
Colorado
Delaware
Florida
Georgia
Idaho
Iowa
Kansas
Kentucky
Maine
Michigan
Minnesota
Missouri
Montana
Nebraska
Ohio
Oregon
Tennessee
Texas
Utah
Vermont
Virginia
```

## The while Command

The while command is a cross between the if-then statement and Linux for loop. It allows you to define a command to test a condition and then looping through a set of commands until you reach a zero exit status. It will analyze the test command at the start of each iteration. Upon reaching the non-zero exit status, the while command stops the execution of the set of commands.

```bash
$ cat test10
#!/bin/bash
# This is a while command test in Linux
var15=20
while [ $var15 -gt 0 ]
do
    echo "This is $var15 in the while loop."
    var15=$var15 - 1
done
```

```bash
$ bash -f main.sh
This is 20 in the while loop.
This is 19 in the while loop.
```
