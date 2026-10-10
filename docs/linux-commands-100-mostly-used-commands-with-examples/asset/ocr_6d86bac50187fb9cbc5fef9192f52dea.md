You can trace a program along with its command-line arguments.

+   10. **Tracing Multiple Commands:**

```
ltrace -o output.txt sh -c "ls; echo Hello"
```

Tracing multiple commands in a shell by using the `c` option and enclosing them in quotes.

+   11. **Displaying Function Arguments:**

```
ltrace -f -F ls
```

The `f` option follows forks, and the `F` option displays function arguments.

# **36. useradd: Create a new user account.**

The `useradd` command in Linux is used to create a new user account on the system. It is a fundamental command, and it allows you to specify various parameters while creating a new user.

**Examples:**

+   1. **Create a new user:**