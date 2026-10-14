
It produces only this strange message. What’s going on? Why didn’t it build the program again? Ah, this is the magic of make. Rather than simply build everything again, make builds only what needs building. With all of the targets present, make determined that there was nothing to do. We can demonstrate this by deleting one of the targets and running make again to see what it does.

```
[me@linuxbox diction-1.1]$ rm getopt.o
[me@linuxbox diction-1.1]$ make
```

We see that make rebuilds getopt.o and relinks the diction and style programs, since they depend on the missing module. This behavior also points out another important feature of make: It keeps targets up-to-date. make insists that targets be newer than their dependencies. This makes perfect sense, as a programmer will often update a bit of source code and then use make to build a new version of the finished product. make ensures that everything that needs building based on the updated code is built. If we use the touch program to “update” one of the source code files, we can see this happen:

```
[me@linuxbox diction-1.1]$ ls -l diction getopt.c
-rwxr-xr-x 1 me me 37164 2009-03-05 06:14 diction
-rw-r--r-- 1 me me 33125 2007-03-30 17:45 getopt.c
[me@linuxbox diction-1.1]$ touch getopt.c
[me@linuxbox diction-1.1]$ ls -l diction getopt.c
-rwxr-xr-x 1 me me 37164 2009-03-05 06:14 diction
-rw-r--r-- 1 me me 33125 2009-03-05 06:23 getopt.c
[me@linuxbox diction-1.1]$ make
```

After make runs, we see that it has restored the target to being newer than the dependency:

```
[me@linuxbox diction-1.1]$ ls -l diction getopt.c
-rwxr-xr-x 1 me me 37164 2009-03-05 06:24 diction
-rw-r--r-- 1 me me 33125 2009-03-05 06:23 getopt.c
```

The ability of make to intelligently build only what needs building is a great benefit to programmers. While the time savings may not be apparent with our small project, it is significant with larger projects. Remember, the Linux kernel (a program that undergoes continuous modification and improvement) contains several million lines of code.

## Installing the Program

Well-packaged source code often includes a special make target called install. This target will install the final product in a system directory for use. Usually, this directory is /usr/local/bin, the traditional location for locally built software. However, this directory is not normally writable by ordinary users, so we must become the superuser to perform the installation:

```
[me@linuxbox diction-1.1]$ sudo make install
```

After we perform the installation, we can check that the program is ready to go:

```
[me@linuxbox diction-1.1]$ which diction
/usr/local/bin/diction
[me@linuxbox diction-1.1]$ man diction
```

And there we have it!

## Final Note

In this chapter, we have seen how three simple commands—./configure, make, make install—can be used to build many source code packages. We have also seen the important role that make plays in the maintenance of programs. The make program can be used for any task that needs to maintain a target/dependency relationship, not just for compiling source code.

## PART 4

WRITING SHELL SCRIPTS

## 24

## WRITING YOUR FIRST SCRIPT

In the preceding chapters, we have assembled an arsenal of command-line tools. While these tools can solve many kinds of computing problems, we are still limited to manually using them one by one on the command line. Wouldn’t it be great if we could get the shell to do more of the work? We can. By joining our tools together into programs of our own design, the shell can carry out complex sequences of tasks all by itself. We enable it to do this by writing shell scripts.

### What Are Shell Scripts?

In the simplest terms, a shell script is a file containing a series of commands. The shell reads this file and carries out the commands as though they have been entered directly on the command line.

The shell is distinctive, in that it is both a powerful command-line interface to the system and a scripting language interpreter. As we will see, most of the things that can be done on the command line can be done in scripts, and most of the things that can be done in scripts can be done on the command line.
