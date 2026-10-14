Now if you run this script, here's what you'll see:

```
```bash
./testvars birds have lips
My name is testvars
First arg is: birds
Second arg is: have
I got a total of 3 arguments
The full argument string was: birds have lips
```
```

# FLOW CONTROL

So far, all of our sample scripts have been just a sequence of commands executed one after the other. We haven't added any if/then/else logic or used looping constructs to control the flow of the program.

+   - **NOTE:** If you've never written or seen a computer program in your entire life, the rest of this chapter will probably seem a bit foreign. But try to follow the examples; then test and modify them on your own to get the hang of it.

# CONDITIONAL OPERATIONS

Let's look at the if/then/else construct in a Bash shell script and see how to control the flow of a script with conditional logic. The general form of if/then/else is shown here, with the actual syntax shown in boldface and the parts you must supply in normal type:

```
```bash
if [ condition is true ]
then
        execute these commands
else
        execute these commands
fi
```
```

The else clause is optional, but you must end the construct with the fi command. You can also have nested if clauses by using the elif command like this:

```
```bash
if [ condition is true ]
then
        execute these commands
elif [ condition2 is true ]
then
        execute these commands
else
        execute these commands
fi
```
```