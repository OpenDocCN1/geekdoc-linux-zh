# 11

# THE ENVIRONMENT

![](bbox=[0.35, 0.24, 0.65, 0.45])

As we discussed earlier, the shell maintains a body of information during our shell session called the *environment*. Programs use the data stored in the environment to determine facts about the system's configuration. While most programs use *configuration files* to store program settings, some programs also look for values stored in the environment to adjust their behavior. Knowing this, we can use the environment to customize our shell experience.

In this chapter, we will work with the following commands:

+   - `printenv` Print part or all of the environment
+   - `set` Set shell options
+   - `export` Export environment to subsequently executed programs
+   - `alias` Create an alias for a command

# What Is Stored in the Environment?

The shell stores two basic types of data in the environment; though, with bash, the types are largely indistinguishable. They are *environment variables* and *shell variables*. Shell variables are bits of data placed there by bash, and environment variables are everything else. In addition to variables, the shell stores some programmatic data, namely, *aliases* and