# 8.8.4 Traps in Functions

If you use a trap to handle a signal in a function, it will affect the entire script, once the function is called. The trap is global to the script. In the following example, the trap is set to ignore the interrupt key, Ctrl-C. This script had to be killed with the kill command to stop the looping. It demonstrates potential undesirable side effects when using traps in functions.

# EXAMPLE 8.57

(The Script)

```
#!/bin/sh
1 trapper () {
    echo "In trapper"
2 trap 'echo "Caught in a trap!"' 2
    # Once set, this trap affects the entire script. Anytime
    # ^C is entered, the script will ignore it.
}
3 while :
    do
        echo "In the main script"
4       trapper
5       echo "Still in main"
        sleep 5
    done
```

(The Output)

```
In the main script
In trapper
Still in main
^C Caught in a trap!
In the main script
In trapper
Still in main
^C Caught in a trap!
In the main script
```

# EXPLANATION

+   1. The trapper function is defined. All variables and traps set in the function are global to the script.
+   2. The trap command will ignore signal 2, the interrupt key (^C). If ^C is pressed, the message Caught in a trap! is printed, and the script continues forever.
+   3. The main script starts a forever loop.
+   4. The function trapper is called.
+   5. When the function returns, execution starts here.