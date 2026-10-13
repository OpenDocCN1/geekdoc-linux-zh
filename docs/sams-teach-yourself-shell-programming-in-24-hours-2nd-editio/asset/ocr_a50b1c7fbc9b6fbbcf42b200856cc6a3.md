# How can I store the output of a command in a variable?

You can store the output of a command in a variable by combining the assignment operator, =, and the backquotes, `:`

```
var=`cmd`
```

Here var is the name of a variable and cmd is the command whose output you want to store. For example, the following command stores the current date in the variable THEDATE:

```
THEDATE=`date`
```

# How do I check to see whether a variable has a value?

There are several methods for determining this. The simplest is the if statement:

```
if [ -z "$VAR" ] ; then
  list ;
fi
```

Here VAR is the name of the variable, and list is the list of commands to execute if VAR does not have a value. Usually list initializes VAR to some default value. For example, the following command initializes the variable THEDATE if it does not have a value:

```
if [ -z "$THEDATE" ] ; then
  THEDATE=`date`
fi
```

If you are just interested in variable initialization, this can be accomplished in a much more succinct fashion using variable substitution. For example, the previous if statement can be written as

```
: ${VAR:=default}
```

Here default is the default that should be assigned to VAR, if VAR does not have a value. If you need to execute a set of commands to obtain a default value, the backquotes (`) can be used to obtain the value to be substituted:

```
: ${VAR:=`default`}
```

Here default is a list of commands to execute. If VAR does not have a value, the output of these commands will be assigned to it. The following command also initializes the variable THEDATE:

```
: ${THEDATE:=`date`}
```