
```bash
echo -e "\n$(date "+%d-%m-%Y --- %T") --- Starting work\n"
apt-get update
apt-get -y upgrade
apt-get -y autoremove
apt-get autoclean
echo -e "\n$(date "+%T")\t Script Terminated"
```

This script will also remove old packages that you do not need anymore. Make sure to run it using `sudo` — if you don't, it won't work.

Shell scripting in Linux isn't as hard as you might think it is, and your scripts can be as diverse as you want. There is no limit in what they can or cannot do and, if you are new to this, new to using Linux and the bash script, take the time to learn these fundamental scripts – they will form the basis of just about everything you want to do. Once you have learned them, take the time to play around with them, change things, learn how they work, and understand exactly what they can do.

I've tried to give you a decent insight into what you need for Linux shell scripting today. The subject goes far deeper than this, though, so I've kept things basic and simple to help you learn. While it isn't too technical, it is a good starting point.

## Chapter Nine

### Linux Shell Scripting for Functions

When you write your scripts, there is every chance that you will use the same code in several locations. If it is a small code, rewriting it isn't such a big deal but, where you have large code that needs to be used in several places, it gets tedious. The bash shell provides the solution -- encapsulation. In this way, the code is encapsulated in a function, and this can be used wherever it is needed throughout the code.

### The Basics

When you start to write more complex scripts, there is every chance that parts of your code performing specific tasks will need to be reused. That could be something as simple as displaying a message multiple times to get answers from users. Or it could be more complex, perhaps complicated calculations that need to be used repeatedly in the script. No matter what it is, having to write the code over and again starts to get tiring, but luckily, the bash shell makes it easy. We simply write the code once and wrap it in a function. Name it according to the contents and, when you need that piece of code anywhere in the script, you can simply call the function name.

### Function Creation

Functions can be created in two formats. The first is using the keyword `function` with the function name assigned to it. The function's name attribute defines the function, but the name should not be one of the reserved keywords; it should be unique and relate to the function contents. The commands are made up of several bash shell commands and when the function is called, the commands are executed in the order they were written in the function.

The second format follows the same function creation pattern used in other programming languages.

```bash
$ cat test15567
#!/bin/bash
function Myfunction1 {
  echo "You are looking at the example of a Linux shell function."
}
count=1
while [ $count -le 10 ]
do
  Myfunction1
  count=$[ $count + 1 ]
done
  echo "You have reached the end of the loop."
  Myfunction1
  echo "This is the finishing point of your Linux shell script. Where do you want to go now?"
$ bash -f main.sh
```

You are looking at the example of a Linux shell function.

You are looking at the example of a Linux shell function.

Repeated eight more times, until the final line of:

You have reached the end of the loop.

You are looking at the example of a Linux shell function.

This is the finishing point of your Linux shell script. Where do you want to go now?

When the name, `Myfunction1`, is referred to, the bash shell returns its definition and the commands defined in it are executed. The definition does not need to be first in the shell script but if you try using a function before the definition, an error message is thrown:

```bash
$ cat test15567
#!/bin/bash
count=1
echo "You are seeing this line that comes before the function definition."

function Myfunction1 {
  echo "You are looking at the example of a Linux shell function."
}

while [ $count -le 10 ]
do
  Myfunction1
  count=$[ $count + 1 ]
done
  echo "You have reached the end of the loop."
  function Myfunction2
  echo "This is a definition of another function"
$ bash -f main.sh
```

You are seeing this line that comes before the function definition.
You are looking at the example of a Linux shell function.
Repeated nine more times, until the final line of:
You have reached the end of the loop.
main.sh: line 1: $: command not found
main.sh: line 17: syntax error near unexpected token `echo'
main.sh: line 17: `echo "This is a definition of another function"'

### Food for thought

When we defined the first function, the shell was defined following a series of commands. When we used `Myfunction1` in the script, it was immediately located by the shell. However, our script attempted to use `Myfunction2` before it had been defined, throwing an error message.

The point here is that a function must be defined before it can be used in a script and you need to be careful about function names. These must be unique, and they must not be keywords. Where a function is redefined, the new definition overrides the previous one. What is important here is that we didn’t get an error message on the screen but something has definitely gone wrong; finding out what it is will be hard and these are all things you need to keep in mind when you start writing Linux scripts.

```bash
$ cat test15567
#!/bin/bash
count=1
function Myfunction1 {
echo "You are looking at the example of a Linux shell function."
}

Myfunction1

function Myfunction1 {
echo "This is a definition of another function"
}
Myfunction1

echo "This Linux script ends here."
$ bash -f main.sh
```

You are looking at the example of a Linux shell function.

This is a definition of another function
This Linux script ends here.

### Returning a Value in Linux Functions

The bash shell tends to treat functions such as mini-scripts that have an exit status. You can generate exit status for functions in three different ways. The exit status by default is something that is returned by the final command in a function. After the execution of the function, you may use the standard `$?` variable to determine its exit status.

### Passing Parameters to a Function

The bash shell treats functions like mini-scripts, which means that you may pass parameters to a function like a regular script. Functions may use a standard parameter environment variables to represent the parameters that are passed to a function on the command line.

```bash
$ cat test6
#!/bin/bash
# In this example, I will be passing parameters to a function
function addmedigits {
if [ $# -eq 0 ] || [ $# -gt 2 ]
then
echo -1
elif [ $# -eq 1 ]
then
echo $[ $1 + $1 ]
else
echo $[ $1 + $2 ]
fi
}
echo -n "I am now Adding 30 and 85: "
valuedigits=$(addmedigits 30 85)
echo $valuedigits
echo -n "Shall we try adding a single number: "
valuedigits=$(addmedigits 10)
echo $valuedigits
echo -n "I am not trying to add any numbers now: "
valuedigits=$(addmedigits)
echo $valuedigits
echo -n "Finally, I am trying to add three numbers: "
valuedigits=$(addmedigits 40 15 90)
echo $valuedigits
bash -f main.sh
```

I am now Adding 30 and 85: 115

Shall we try adding a single number: 20

I am not trying to add any numbers now: -1

Finally, I am trying to add three numbers: -1

The `addmedigits` function checks the number of parameters that are passed to the function. If there are no parameters or more than two parameters, the value is returned as -1. If there is a single parameter, it adds that to itself for the result. If there are two parameters, it adds all of them for the result. Since the function uses a special parameter environment variable for its parameter values, it cannot access the script parameter values from the command line of the script.

### Passing Arrays to Functions

Passing arrays into functions is a precise art but, to start with, it may be confusing. If an array variable is passed as a single variable, it will not work:

```bash
$ cat badtest3
#!/bin/bash
function func555 {
echo "The parameters being used in the function are: $@"
myarray=$1
echo "The array that is received is as follows: ${myarray[*]}"
}
thisarray=(1 2 3 4 5 6 7 8 9 10)
echo "This is the original array : ${thisarray[*]}"
func555 $thisarray
$ bash -f main.sh
```

This is the original array : 1 2 3 4 5 6 7 8 9 10

The parameters being used in the function are: 1

The array that is received is as follows: 1

If you try to use the array variable as a function parameter, the function takes the first value in the array variable. Fixing this requires that the array variable is broken down into its individual values, which are then used as function parameters. You can reassemble those parameters in the function as a new array variable. Here’s an example:

```bash
$ cat test10
#!/bin/bash
function testingfunction {
```
