
## Sharing Functions Between Subprograms

Say that you create a program that uses the function that verifies an ID and password, as I describe in the preceding section. But you also want to use the same function in another program that doesn’t contain the function. Instead of copying the function into the second program, you can make the function in your first program available to the second program.

You can share functions between subprograms by using the export command to export the function. You then call the subprogram from within your second program. The following example shows you how to do so:

```bash
#!/bin/bash
clear
function verify
{
  if [ $# -ne 2 ]
  then
    echo "Wrong number of arguments!"
  else
    if [ $1 -eq "Bob" ] && [ $2 -eq "565" ]
    then
      echo "Verified"
    else
      echo "Rejected"
    fi
  fi
}
export verify
subprogram1
```

Following is a description of what you add to the last lines of the function definition to share the function:

- 1. Following the closing brace that ends the function definition, you use the export command to make the verify function available to the subprogram that I call subprogram1.
- 2. The last line of the program calls subprogram1, which the following example shows. Notice that subprogram1 doesn’t contain the function definition for verify, but the subprogram calls the verify function, because the export command exports the verify function before calling the subprogram.

```bash
#!/bin/bash
clear
verify "Bob" "565"
```

### Returning Information from a Function

A function is like a two-way street because you can send information to the function and the function can send information back to your program. Say that, instead of the verify function displaying a message stating whether the ID and password are valid, the verify function sends the results to your program. Your program can then decide the appropriate action to undertake.

Your program assigns the information that a function returns to the `$?` variable. The value of that information must be an integer from 0 to 256. You can’t, therefore, send a string as a return value of a function.

Your program sends a value back from a function by using the return keyword, following it with the value that it’s returning. Because the return value is an integer, you must assign meaning to each integer that’s returning. You typically use a zero, for example, to indicate that the function is operating correctly. Any other integer indicates that something’s wrong.

You can place a return anywhere in your function, but the return usually falls somewhere in the program after the place where function tests the values — such as where the program compares the ID and password. After Linux executes return, the function stops executing and Linux returns to the line in the program that calls the function.

The following example shows you how to return a value from a function:

```bash
#!/bin/bash
clear
function verify
{
    if [ $# -ne 2 ]
    then
        return 1
    else
        if [ $1 -eq "Bob" ] && [ $2 -eq "555" ]
        then
            return 0
        else
            return 2
            echo "Rejected"
        fi
    fi
}
verify Bob 555
case $? in
    0)
        echo "Verified"
        ;;
    1)
        echo "Wrong number of arguments!"
        ;;
    2)
        echo "Rejected"
        ;;
done
```

The following steps describe what's happening in this program:

- 1. The `bash` shell starts.
- 2. The screen clears of unnecessary information.
- 3. The program defines the function `verify`.
- 4. Following the opening brace, the program compares the number of arguments passed to the function with the value `2`. If the count is not 2, the function returns a value of `1`.
- 5. If it receives the correct number of arguments, the program compares the value of variable `$1` with "Bob" and the value of variable `$2` with "555". `$1` is the ID passed to the function. `$2` is the password passed to the function. "Bob" is the valid ID, and "555" is the valid password.
- 6. The function returns a `0` or a `2` depending on whether the correct ID and password are passed to the function.
- 7. Following the closing brace that ends the function definition, the program calls the function and passes "Bob" as the ID and "555" as the password.
- 8. The program uses the `case` statement to compare the `$?` variable that contains the `return` value with values in the `case` statement.

![](img/05279073f26be7df99b3c487360dec6a_166_0.png)

### Test Your Programming Knowledge

1. When do you use a function?
    - a. Whenever you find yourself repeating code in your program.
    - b. Whenever you want to give yourself a raise.
    - c. Whenever you get tired of typing.
    - d. Whenever you want to copy instructions.

2. What information can a function return?
    - a. Any characters or numbers.
    - b. Characters only.
    - c. An integer between 0 and 256.
    - d. The winning lottery number.

**Answers:**
1. a. See “Creating a Function.”
2. c. See “Returning Information from a Function.”

# Chapter 14
# Getting Down with Subprograms

## In This Chapter

- Creating a program plan
- Creating subprograms
- Naming subprograms
- Using subprograms
- Sharing subprograms

Although you design each program to perform a specific task, every program that you write shares some basic functions in common with other programs. Every program, for example, displays text on a screen, reads information that a user enters on the keyboard, saves the user’s input to a variable, and then works with the information.

You piece each of these tasks together to build large, complex programs that tell the computer to perform some useful tasks. At times, you want your program to perform a specific group of related tasks, such as displaying an error message on-screen if the user does something wrong with your program.

Pretty soon, you’re writing Linux programs that enable your computer to do all sorts of fancy things.

Because errors can occur practically anywhere in your program, duplicating the necessary instructions to display an error message throughout your program doesn’t make sense. Such duplication takes up too much space and is a nightmare to maintain. Every time that you change a part of the error message, you must remember all the places in your program where you duplicate those instructions.

You can avoid the problems that result from duplicate instructions in your program simply by placing those instructions in a small program known as a subprogram. A subprogram is identical to a regular program in that you create a subprogram by using an editor and the chmod command to transform the file into an executable program (a file that your computer can run).

The only thing special about a subprogram is that the instructions you place in a subprogram are those that you design to perform a *specific* task, such as displaying an error message or checking for the correct user's password. Those same subprograms can then execute from within your program whenever you need it to perform a special task.

You often find yourself building large, complex programs from many subprograms. To make sure that your program works smoothly and is also easy to read, however, you need to *map out* the tasks that you want your program to perform and then decide how each task relates to the other tasks in the program. In this chapter, I take you through the steps for creating an overall program plan and describe how subprograms contribute to a well-designed and efficient program.

## Why Use a Subprogram?

Subprograms are the building blocks of your program. First, you create each building block, and then you assemble them to develop the whole program.

Suppose that you need the computer to display an opening menu and respond to whatever the user selects. You call both of these activities one task, because whenever a menu appears, the program always waits for a response from the user. You can place all the code that's necessary to perform this task into the same subprogram. Your program then calls this subprogram whenever you want to perform the task.

The following list describes some reasons for using subprograms:

- Subprograms isolate all code performing a specific task. If you're having a problem with your menu display, for example, you don't need to hunt through your entire program for the piece of code that's causing the problem. You just need to look in the display-menu subprogram.
- Building your program from subprograms saves you from repeating the code in your program. You simply execute the subprogram whenever you need the program to perform that task.
- You make changes or updates to code in just one place in your program. (*What a timesaver!*)
- Subprograms are reusable, and you can use them to build other Linux programs — and share them with other programmers who want their programs to perform some of the same tasks that your program performs.
