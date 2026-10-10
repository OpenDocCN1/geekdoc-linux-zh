zmodload command line:

```
```
% zmodload zsh/net/tcp
%
```
```

Nothing indicates that the module loaded. You can perform another zmodload command, and the new module should appear in the list of installed modules. Once you load a module, the commands associated with the module are available as built-in commands.

> **TIP**
> 
> **It’s a common practice to place zmodload commands in the $HOME/.zshrc startup file so that your favorite functions load automatically when the zsh shell starts.**

# ### Scripting with zsh

The main purpose of the zsh shell was to provide an advanced programming environment for shell programmers. With that in mind, it’s no surprise that the zsh shell offers many features that make shell scripting easier.

# #### Mathematical operations

As you would expect, the zsh shell allows you to perform mathematical functions with ease. In the past, the Korn shell has led the way in supporting mathematical operations by providing support for floating-point numbers. The zsh shell has full support for floating-point numbers in all of its mathematical operations!

# ##### Performing calculations

The zsh shell supports two methods for performing mathematical operations:

+   - The let command
+   - Double parentheses