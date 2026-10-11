If you want to remove a directory from the stack, you can use the popd built-in provided by the C shell. If popd is used without an argument, it will remove the top directory from the stack. The working directory would then become the top directory. Figure 20.4 illustrates how popd removes a directory from the stack. If you want to remove a directory from somewhere else in the stack, you can use a numeric argument, just as you did with pushd. Keep in mind that the top directory is always zero, so begin counting with 0 and precede the number with a + sign as in the following example:

```
```
% popd +1
~/music ~/tape
% pwd
/home/barrie/music
```
```

# **FIGURE 20.4**

![](bbox=[0.07, 0.41, 0.72, 0.66])

The use of these built-ins will aide you in manipulating your directory stacks with ease. You will save time by getting accustomed to their use.

# ## C Shell Variables

The C shell sets some variables, retains some that are inherent in the environment, and uses some that are set by the user. Most of the variables listed in this section belong uniquely to the C shell, though a few may be used by other shells. Some shell variables have significant values such as the PID number. Some shell variables act as