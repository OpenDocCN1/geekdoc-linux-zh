You use this statement type to notify users in a specific *classname* that the file exists, and/or that changes were made since they last connected. A full **readme** statement might be as complex as the following:

```
readme path when classname
```

The arguments used for **readme** are:

+   *   **path**—The path to the file you want to have monitored.
+   *   **when**—This item can be one of two different choices. The first text you can use here is **LOGIN**, which tells **wu-ftpd** to use this **readme** statement whenever someone meeting its rules logs in. The second option is **CWD=path**. Using this choice tells **wu-ftpd** to process this **readme** statement whenever an FTP user uses the **cwd** (change working directory) command to the specified location.
+   *   **classname**—A previously defined *classname* from a **class** statement. Optional.

Next is the following pair of lines:

```
message /welcome.msg                login
message .message                    cwd=*

```

A **message** statement enables you to specify text that is displayed the moment someone logs in or changes into a directory. You can use this statement in the following format:

```
message path when classname
```

The arguments for **message** are the same as they are for **readme**. What follows is a collection of statements that all use a similar format:

compress				yes				all
tar										yes				all
chmod										no				guest,anonymous
delete										no				guest,anonymous
overwrite									no				guest,anonymous
rename										no				guest,anonymous


The first two lines involve file extensions. A **compress** statement refers to Z or GZ files, whereas **tar** refers to TAR files. In both cases, these commands are used in this format:

```
*extension* *command* *active* *who*
```