# bash
programming

Shell programs are simple text files containing some Linux and/or bash commands. After the start of a shell program, these commands are executed one after the other. The shell program can be passed parameters, as with with any normal command. Parameters can be evaluated inside the program.

Since the sequential execution of a few commands does not leave much room for complex tasks, the bash supports shell programming with commands for the construction of loops and branches. With this, you have a true programming language at your disposal which need neither a compiler nor knowledge of C; Admittedly, this comparison is a bit lame: C programs execute much faster, support several types of variables, offer a large number of special functions, and so on. Nevertheless, the possibilities of the bash are more than sufficient to cope with a surprisingly high number of problems.

Typical applications of shell programs are the automation of frequently needed command sequences for installation of programs, system administration, creation of backups, configuration and execution of single programs, and so forth.

> NOTE This chapter builds on the bash fundamentals laid out in Chapter 12. In particular, you should be familiar with input and output redirection, command substitution and the handling of variables.

# 13.1 Introduction

Let us assume that you frequently enter the command ls -ltr in order to create a list of files in the current directory ordered by date (the most recent file last). Each time, you try again to remember which combination of options will get you there. Thus,