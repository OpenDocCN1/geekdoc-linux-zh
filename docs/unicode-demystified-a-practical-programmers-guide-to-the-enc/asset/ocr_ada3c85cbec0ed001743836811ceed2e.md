# Do Not Name Your Shell Script test

You can create a problem for yourself if you give a shell script name test. A GNU/Linux utility has the same name. Depending on how you have your PATH variable set up and how you call the program, you may run your script or the utility, leading to confusing results.

This chapter illustrates concepts with simple examples followed by complicated examples in sections marked “Optional”. The more complex scripts illustrate traditional shell programming practices and introduce some GNU/Linux utilities used in scripts. You can skip these sections without loss of continuity the first time you read the chapter. Return to them later when you feel comfortable with the basic concepts.

# Control Structures

The control flow alters the order of execution of commands within a shell script. The Bourne Again and Z Shells share a common syntax, whereas the TC Shell uses a different syntax (page 714). Control structures include the if...then, for...in, while, until, and case statements. In addition, the break and continue statements work in conjunction with the control flow structures to alter the order of execution of commands within a script.

if...then the syntax of the if...then control structure is

```
test-command
then
commands
```

The bold words in the syntax description are the items you supply to cause the structure to have the desired effect. The nonbold words are the keywords the shell uses to identify the control structure.

Figure 13-1 shows that the if statement tests the status returned by the test-command and transfers control based on this status. The end of the if structure is marked by a fi statement, which is if spelled backward. The following script prompts you for two words, read them in, and uses an if structure to evaluate the result returned by the test builtin when it compares the two words.