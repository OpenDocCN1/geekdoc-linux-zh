
The CGI (Common Gateway Interface) allows external application programs to interface with Web servers. Any program can be a CGI program if it runs in real time and relays its output to the requesting client.

SSL (Secure Sockets Layer) has two functions: It allows a client to verify the identity of a server and it enables secure two-way communication between a client and server.

## EXERCISES

- 1. What is Apache? Very basically, how does it work (i.e., what happens when you point a browser at a Web page)?
- 2. What is the function of the document root? Where is it located by default? How would you change the location of the document root?
- 3. How would you tell Apache that the content is in `/usr/local/www`?
- 4. How would you instruct an Apache server to listen on port 81 instead of port 80?
- 5. How would you enable Sam to publish Web pages from his `~/website` directory but not allow anyone else to publish to the Web?
- 6. Apache must be started with `root` privileges. Why? Why does this action not present a security risk?
- 7. What is the relationship between Apache and `httpd`?
- 8. What does the `ServerName` directive do? Which value can you use as a `ServerName` if you want to experiment with an Apache server locally (on the server system)?

## ADVANCED EXERCISES

- 9. If you are running Apache on a firewall system, perhaps to display a Web front end for firewall configuration, how would you make sure that it is accessible only from inside the local network?
- 10. Why is it more efficient to run scripts using `mod_perl` than to run them through CGI?
- 11. What two things does SSL provide, and how does this situation differ if the certificate is self-signed?
- 12. Some Web sites generate content by retrieving data from a database and inserting it into a template using PHP or CGI each time the site is accessed. Why is this practice often a poor idea?
- 13. Assume you want to provide Webmail access for employees on the same server that hosts the corporate Web site. The Web site address is example.com, you want to use mail.example.com for Webmail, and the Webmail application is located in /var/www/webmail. Describe two ways you can set up this configuration.
- 14. Part of a Web site is a private intranet. Describe how you would prevent people outside the company's internal 192.168.0.0/16 network from accessing this site. The site is defined as follows:

```
<VirtualHost *:80>
  ServerName example.com
  DocumentRoot /var/www
  <Directory /var/www/intranet>
      AllowOverride AuthConfig
  </Directory>
</VirtualHost>
```

- 15. What is a container? Give an example of container syntax.
- 16. What does CGI do? What are the characteristics of a CGI program?
- 17. What are the functions of SSL?

# PART V: PROGRAMMING TOOLS

## CHAPTER 27
Programming the Bourne Again Shell (Bash) 981

## CHAPTER 28
The Python Programming Language 1081

## CHAPTER 29
The MariaDB SQL Database Management System 1113

*This page intentionally left blank*

# 27
## Programming The Bourne Again Shell (bash)

### In This Chapter

- Control Structures . . . . . . . . . . 982
- File Descriptors . . . . . . . . . . . . . . 1016
- Positional Parameters . . . . . . . . . 1022
- Special Parameters . . . . . . . . . . . 1027
- Variables . . . . . . . . . . . . . . . . . . . . . 1031
  - Environment, Environment Variables, and Inheritance . . . . 1032
  - Array Variables . . . . . . . . . . . . . 1038
- Builtin Commands . . . . . . . . . . . . . 1040
- Expressions . . . . . . . . . . . . . . . . . . 1056
- Shell Programs . . . . . . . . . . . . . . . 1064
- A Recursive Shell Script . . . . . . . 1065
- The quiz Shell Script . . . . . . . . . . . 1068

### Objectives

After reading this chapter you should be able to:

- Use control structures to implement decision making and repetition in shell scripts
- Handle input to and output from scripts
- Use shell variables (local) and environment variables (global)
- Evaluate the value of numeric variables
- Use `bash` builtin commands to call other scripts inline, trap signals, and kill processes
- Use arithmetic and logical expressions
- List standard programming practices that result in well-written scripts

Chapter 5 introduced the shells and Chapter 9 went into detail about the Bourne Again Shell. This chapter introduces additional Bourne Again Shell commands, builtins, and concepts that carry shell programming to a point where it can be useful. Although you might make use of shell programming as a system administrator, you do not have to read this chapter to perform system administration tasks. Feel free to skip this chapter and come back to it if and when you like.

The first part of this chapter covers programming control structures, also called control flow constructs. These structures allow you to write scripts that can loop over command-line arguments, make decisions based on the value of a variable, set up menus, and more. The Bourne Again Shell uses the same constructs found in programming languages such as C.

The next part of this chapter discusses parameters and variables, going into detail about array variables, shell versus environment variables, special parameters, and positional parameters. The exploration of builtin commands covers `type`, which displays information about a command, and `read`, which allows a shell script to accept user input. The section on the `exec` builtin demonstrates how to use `exec` to execute a command efficiently by replacing a process and explains how to use `exec` to redirect input and output from within a script.

The next section covers the `trap` builtin, which provides a way to detect and respond to operating system signals (such as the signal generated when you press CONTROL-C). The discussion of builtins concludes with a discussion of `kill`, which can abort a process, and `getopts`, which makes it easy to parse options for a shell script. Table 27-6 on page 1055 lists some of the more commonly used builtins.

Next the chapter examines arithmetic and logical expressions as well as the operators that work with them. The final section walks through the design and implementation of two major shell scripts.

This chapter contains many examples of shell programs. Although they illustrate certain concepts, most use information from earlier examples as well. This overlap not only reinforces your overall knowledge of shell programming but also demonstrates how you can combine commands to solve complex tasks. Running, modifying, and experimenting with the examples in this book is a good way to become comfortable with the underlying concepts.

### Do not name a shell script test

> **Tip**: You can unwittingly create a problem if you name a shell script `test` because a `bash` builtin has the same name. Depending on how you call your script, you might run either your script or the builtin, leading to confusing results.

![](img/243613168ac865b539f12460d966088e_1038_0.png)

### CONTROL STRUCTURES

The *control flow* commands alter the order of execution of commands within a shell script. Control structures include the *if*... *then*, *for*... *in*, *while*, *until*, and case statements. In addition, the **break** and **continue** statements work in conjunction with the control structures to alter the order of execution of commands within a script.

You can use the **bash help** command to display information within **bash** control structures. See page 134 for more information.

#### if...then

The **if...then** control structure has the following syntax:

```
if *test-command*
    then
        *commands*
fi
```

The **bold** words in the syntax description are the items you supply to cause the structure to have the desired effect. The *nonbold* words are the keywords the shell uses to identify the control structure.

Figure 27-1 shows that the if statement tests the status returned by the *test-command* and transfers control based on this status. The end of the if structure is marked by a fi statement (*if* spelled backward). The following script prompts for two words, reads them, and then uses an if structure to execute commands based on the result returned by the **test** builtin when it compares the two words. (See the **test info** page for information on the **test** utility, which is similar to the **test** builtin.) The **test** builtin returns a status of
