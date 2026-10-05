# Chapter 4 Creating a Basic Sendmail Configuration

**WARNING** A quoted string in the argument field of m4 macro must begin with ` ` and end with ` `. This is important. If other quotes marks are used, you will have errors in your configuration.

**FEATURE** The macro identifies an optional Sendmail feature for inclusion in the sendmail.cf file. A single m4 file can contain several FEATURE commands. The format of the m4 macro is:

```
FEATURE(`feature-name`, [`parameter`[, [`parameter`...])
```

*Feature-name* identifies the requested feature. Next to that are more than 40 Sendmail features available, all of which are listed in Appendix A. Some of these features parameters used to configure those features, are used in this book. Next to the define command, the FEATURE command is the most heavily used command in m4 configuration.

**define** the define command is used to set the value of a configuration variable for the sendmail.cf file. As you will see in Chapter 7, “The sendmail.cf file,” this file contains hundreds of variables called macros, classes, and options. The define command identifies the variable by name and sets the value for the variable using this format:

```
define(`variable-name`, `value`)
```

There are hundreds of variable names, most of which you will never use. The important ones are covered in examples in the text. A full list is provided in Appendix A.

**undef** The undef command is the opposite of the define command. It returns the value of a variable to the system default. Thus, the only argument provided to the undef command is the variable name:

```
undef(`variable-name`)
```

At first glance, the undef command may seem odd. Why would you define a value only to undefine it? The answer is, you didn't define it in the first place—someone else did. Configurations are built by bringing together several m4 files that already exist. An existing file may have several values you want for your configuration, and a few you don't want. The undef command lets you use you from the m4 source file while resetting the values you don't want.

The basic configuration commands appear in an m4 configuration file in the following order:

+   - VERSIONID, when used, is the first macro in the m4.
- OTYPE is defined before the other essential macros.