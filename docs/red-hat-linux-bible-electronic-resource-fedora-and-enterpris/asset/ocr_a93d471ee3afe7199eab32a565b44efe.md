# ## Setting up the configuration

To begin reconfiguring the kernel, you should be in a bash shell. (If you are not sure, type `bash` at the command line.) Then go to the `/usr/src/linux-2.4*` directory and type:

```
# make mrproper
```

This prepares you to create the new kernel configuration. It thoroughly cleans up the kernel configuration directories.

# ## Making the configuration

To choose the kernel options that you want, you must run `make` with the `config`, `menuconfig`, or `xconfig` options. By far, the easiest option is `xconfig`, though it requires that you run an X desktop (such as GNOME or KDE). Here is an example:

```
# make xconfig
```

If you are not running X, you can use `config` or `menuconfig`. Using `make config` presents you with a pure text-based, question-and-answer way of rebuilding your kernel. Typing `make menuconfig` from `/usr/src/linux-2.4*` provides a menu-driven interface (which runs in a character terminal).

Besides being a bit nicer to look at, the `menuconfig` and `xconfig` kernel configuration tools enable you to select only those areas of the kernel that you want to change. With `make config`, you have to step through each category. With the `xconfig` tool, you see all selections available in a category. Keep in mind, though, that if a category is turned off, selections within that category are grayed out. Also, if you make a mistake, just reselect the category.

> **NOTE:** You might want to edit the Makefile file at this point and change the value of `EXTRAVERSION`. This can protect you from writing over your original kernel files by mistake. After the new kernel is booted, you can type `uname -a` to see the value of `EXTRAVERSION` appended to the kernel name that is running.

# ## Checking for dependencies

When you have configured the kernel, save the changes. After you have made the kernel configuration changes that you want, you must return to the `/usr/src/linux*` directory and type the following:

```
# make dep
```

The `make dep` command checks that dependencies of the packages are met. Next, you must prepare the source tree.

# ## Preparing the source tree

To prepare the source tree for the new kernel build, run the `make clean` command as follows:

```
# make clean
```