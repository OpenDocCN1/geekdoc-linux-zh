> TIP
> If you are new to the command line and the Linux directory structure, it is recommended that you stick with absolute directory references for a while. After you become more familiar with the directory layout, switch to using relative directory references.

You can use a relative directory reference with the `cd` command in any directory containing subdirectories. You can also use a special character to indicate a relative directory location.

The two special characters used for relative directory references are

+   - The single dot (`.`) to represent the current directory
+   - The double dot (`..`) to represent the parent directory

You **can** use the single dot, but it doesn't make sense to use it with the `cd` command. Later in the chapter, you see how another command uses the single dot for relative directory references effectively.

The double-dot character is extremely handy when you're trying to traverse a directory hierarchy. For example, if you are in the `Documents` directory under your home directory and need to go to your `Downloads` directory, also under your home directory, you can do this:

```
[rich@rocky9 Documents]$ pwd
/home/rich/Documents
[rich@rocky9 Documents]$ cd ../Downloads
[rich@rocky9 Downloads]$ pwd
/home/rich/Downloads
[rich@rocky9 Downloads]$
```

The double-dot character takes you back up one level to your home directory; then the `/Downloads` portion of the command takes you back down into the `Downloads` directory. You can use as many double-dot characters as necessary to move around. For example, if you are in your home directory (`/home/rich`) and want to go to the `/etc` directory, you could type the following:

```
[rich@rocky9 ~]$ cd ../../etc
[rich@rocky9 etc]$ pwd
/etc
[rich@rocky9 etc]$
```

Of course, in a case like this, you actually have to do more typing rather than just typing the absolute directory reference, `/etc`. Thus, use a relative directory reference only if it makes sense to do so.

> Note
> It's helpful to have a long informative shell CLI prompt, as used in this chapter section. However, for clarity purposes, a simple `$` prompt is used in the rest of the book's examples.