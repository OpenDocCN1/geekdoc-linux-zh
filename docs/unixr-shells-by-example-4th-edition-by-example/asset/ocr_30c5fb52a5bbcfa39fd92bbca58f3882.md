# EXAMPLE 8.18 (CONTINUED)

```
2 if [ $age -lt 0 -o $age -gt 120 ]
then
    echo "Welcome to our planet! "
    exit 1
fi
```

```
3 if [ $age -ge 0 -a $age -lt 13 ]
then
    echo "A child is a garden of verses"
elif [ $age -ge 13 -a $age -lt 20 ]
then
    echo "Rebel without a cause"
elif [ $age -ge 20 -a $age -lt 30 ]
then
    echo "You got the world by the tail!!!"
elif [ $age -ge 30 -a $age -lt 40 ]
then
    echo "Thirty something..."
```

```
4 else
    echo "Sorry I asked"
```

```
5 fi
```

(The Output)

```
$ tellme
How old are you? 200
Welcome to our planet!
$ tellme
How old are you? 13
A child is a garden of verses
$ tellme
How old are you? 55
Sorry I asked
```

# EXPLANATION

1 The user is asked for input. The input is assigned to the variable age.

2 A numeric test is performed within the square brackets. If age is less than 0 or greater than 120, the echo command is executed and the program terminates with an exit status of 1. The interactive shell prompt will appear.

3 A numeric test is performed within the square brackets. If age is greater than or equal to 0 and less than 13, the test command returns exit status 0, true, and the statement after the then is executed. Otherwise, program control goes to the elif. If that test is false, the next elif is tested.

4 The else construct is the default. If none of the above statements are true, the else commands will be executed.

5 The fi terminates the initial if statement.