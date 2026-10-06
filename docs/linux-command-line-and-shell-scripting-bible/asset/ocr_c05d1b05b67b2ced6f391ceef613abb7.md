# # Chapter 9

# Using Structured Commands

In the shell scripts presented in Chapter 8, the shell processed each individual command in the shell script in the order it appeared. This works out fine for sequential operations, where you want all of the commands to process in the proper order. However, this isn't how all programs operate.

Many programs require some sort of logic flow control between commands in the script. This means that the shell executes certain commands given one set of circumstances, but it has the ability to execute other commands given a different set of circumstances. There is a whole class of commands that allows the script to skip over or loop through commands based on conditions of variable values, or the result of other commands. These commands are referred to as structured commands.

The structured commands allow you to alter the flow of operation of the program, executing some commands under some conditions, while skipping others under other conditions. There are quite few structured commands available in the bash shell, so we'll look at them individually. In this chapter, we'll look at the if-then statement.

| IN THIS CHAPTER |
| Altering command flow |
| Using if-then logic |
| Nesting if-thens |
| Testing conditions |
| Advanced if-then features |

# ## Working with the if-then Statement

The most basic type of structured command is the if-then statement. The if-then statement has the following format:

```
if command
then
    commands
fi
```