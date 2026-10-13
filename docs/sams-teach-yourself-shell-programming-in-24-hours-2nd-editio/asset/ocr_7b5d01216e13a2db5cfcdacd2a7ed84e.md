Before posting to the mailing list, you should read the zsh FAQ located at http://www.faqs.org/faqs/unix-faq/shell/zsh/

The following Web sites are also excellent references for shell programming:
http://www.h.eng.cam.ac.uk/~help/tpl/unix/scripts/scripts.html
http://www.shelldorado.com/

The first site contains a tutorial on shell programming written by Tim Love at Cambridge University. The second site is an archive of shell scripts and shell programming information maintained by Heiner Steven of Sun Microsystems.

# Summary

This chapter covered what the shell is and how it operates in greater detail. The init process for the various shells was described along with a brief description of the basic information required in the init file .profile. The different modes of operation for the shell, interactive and non-interactive, were also covered. Shell programming relies on the non-interactive mode because it enables commands specified in a file to be executed.

We also covered man and man pages, the online help system in UNIX. Finally, online sources for shell programming information, such as Usenet newsgroups, Web sites, and e-mail lists, were covered.

The next chapter formally introduces the concept of files by showing you how to list files, view the contents of files, and manipulate files.

# Questions

+   1. What are the two files used by the shell to initialize itself?
+   2. Why do you need to set PATH and MANPATH?
+   3. What is the purpose of the following line in a shell script?
+      `#!/bin/sh`
+   4. What command should you use to access the online help?

```
#!/bin/sh
```

# Terms

**Commands** A command is comprised of the name of a program along with zero or more arguments. You might see the term command used instead of the term utility for simple commands, where only the program name is given.

![](bbox=[0.88, 0.3, 0.98, 0.45])