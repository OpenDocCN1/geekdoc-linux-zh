True to its origin as a system administration tool, Perl has been popular with UNIX system administrators for many years. More recently, when the World Wide Web (or Web for short) became popular and the need for Common Gateway Interface (CGI) programs arose, Perl became the natural choice for those already familiar with the language. The recent surge in Perl's popularity is primarily due to the use of Perl in writing CGI programs for the Web. Of course, as people pay more attention to Perl, they discover that Perl is useful for much more than CGI programming. That, in turn, has made Perl even more popular among users.

Perl is available on a wide variety of computer systems because, like the Linux operating system, Perl can be distributed freely.

If you are familiar with shell programming or the C programming language, you can pick up Perl quickly. If you have never programmed, becoming proficient in Perl may take a while. I encourage you to start with a small subset of Perl's features and to ignore anything you don't immediately understand. Then, slowly add Perl features to your repertoire.

# Determining Whether You Have Perl

Before you proceed with the Perl tutorial, check whether you have the perl program installed on your Red Hat Linux system. Type the following command:

```
which perl
```

The which command tells you whether it finds a specified program in the directories listed in the PATH environment variable. If perl is installed, you should see the following output:

```
/usr/bin/perl
```

If the which command complains that no such program exists in the current PATH, that doesn't necessarily mean you don't have perl installed; it may mean simply that you don't have the /usr/bin directory in PATH. Ensure that /usr/bin is in PATH; check by typing the following command:

```
echo $PATH
```

See if the output lists the /usr/bin directory. If /usr/bin is not in PATH, use the following command to redefine PATH:

```
export PATH=$PATH:/usr/bin
```