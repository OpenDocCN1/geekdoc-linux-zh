# Configuring the Package

Most packages ship with an autoconfiguration script; it is safe to assume they do unless their documentation says otherwise. These scripts are typically named “configure,” and they take parameters. There are a handful of stock parameters that are available across all configure scripts, but the interesting stuff occurs on a program-by-program basis. Each package will have a handful of features that can be enabled or disabled or have special values set at compile time, and they must be set up via configure.

To see what configure options come with a package, simply run

```
    [root@ford ssh-2.0.13] # ./configure --help
```

Yes, those are two dashes (“--”) before the word “help.”

In the case of SSH we’ll see a long list of features that can be enabled and disabled. (See Chapter 17 for an explanation of what the options mean with respect to SSH.)

One commonly available option is --prefix. This option allows you to set the base directory where the package gets installed. By default, most packages use /usr/local. Each component in the package will install into the appropriate directory in /usr/local. For example, the server component of SSH is called sshd, which gets installed into /usr/local/sbin.

With all of the options you want set up, a final run of configure will create a special type of file called a “makefile.” Makefiles are the foundation of the compilation phase.

# Compiling Your Package

Compiling your package is the easy part. All you need to do is run make, like so:

```
    [root@ford ssh-2.0.13] # make
```

The make tool reads all of the makefiles that were created by the configure script. These files tell make which files to compile and the order in which to compile them—which is crucial since there could be hundreds of source files.

Depending on the speed of your system, the available memory, and how busy it is doing other things, the compilation process could take a while to complete, so don’t be surprised.

As make is working, it will display each command it is running, with all the parameters associated with it. This output is usually the invocation of the compiler and all of the parameters passed to the compiler—it’s pretty tedious stuff that even the programmers were inclined to automate!

If the compile goes through smoothly, you won’t see any error messages. Most compiler error messages are very clear and distinct, so don’t worry about possibly missing an error. If