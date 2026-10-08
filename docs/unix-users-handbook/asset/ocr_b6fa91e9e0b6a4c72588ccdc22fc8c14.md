If you wish to compile a file called **program** with the **cc** com- mand on a UNIX system, you must issue the following command:

```
`cc program`
```

If you were to issue one of the following commands, you would not compile the desired program:

```
```
CC program
cc Program
```
```

The first example would not run the desired program called **cc**, because **CC**, with uppercase characters, is different from **cc** with low- ercase characters. In the second example, the desired compiler called **cc** would indeed be invoked; however, the file called **Program** that we have specified is different from the desired file called **program**.

In addition to using care with uppercase and lowercase on UNIX systems, you also need to be aware of the fact that there are different file types on UNIX systems. Some different types of files found on UNIX systems, as well as how to determine the type of file you are dealing with, are covered in Chapter 2.

# ## Login Process

All users on a UNIX system have a login name set up for them by the system administrator. The system administrator may consult you on the login name you wish to use. You gain access to the system by sup- plying both your login name and password. I cover this process shortly.

The rules for the login name you choose are determined by your system administrator. Typically, a login name will be two to eight