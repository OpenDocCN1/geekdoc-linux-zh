
![](img/c75d0c4fa51711b62f211459ae794f3f_25_0.png)

**FIGURE 1-4**
This is a common situation—the user fills in a form and gets data from the database.

![](img/c75d0c4fa51711b62f211459ae794f3f_25_1.png)

**FIGURE 1-5**
Each number refers to a point below.

- 1. The user types a Web address in a Web browser (the client) to access the site. This connection also requests the HTML page containing the HTML form.
- 2. The browser connects to the Apache server, which has the HTML and PHP files that form the Web site. Apache services the request (by following the rules in its configuration file to find the relevant page and send it back) and sends the client the Web page containing the HTML form.
- 3. The user fills in the form (in the Web browser) and submits the form to the server.
- 4. The Apache server receives the submitted form and loads the relevant file to handle the form submission. This file contains PHP code that is used to connect to the database. This PHP code is passed to the PHP interpreter by Apache and run by the interpreter. PHP connects to the MySQL database (which may be on the same computer or another one; it doesn't matter which). When connected to the MySQL database, a request is made for the information by using SQL, which is a language designed for communicating with databases.
- 5. The MySQL database receives the SQL request and finds the information. When the information is located, the result is sent back to the PHP script that made the request.
- 6. The PHP script receives the result from the MySQL server and constructs an HTML page with the results included before sending it back to the Web browser client.
- 7. The Web browser receives the HTML result of the query and displays it to the user.

Throughout this process, you'll want to bear in mind a few key items. It is recommended that you read the following key points and then review the preceding process to clarify any confusion.

To begin, the Web browser understands hypertext only; it does not understand PHP. (Of course, the former is the assumption that one makes for all Web browsers because they all are built to understand hypertext. Some browsers may understand scripting languages such as JavaScript, but that example is out of the scope of this discussion.) All communication to and from the Web browser is done in hypertext (hence converting the results of the MySQL query to hypertext in Step 6). Another point is that PHP is tightly linked to Apache on the server, and all database connections/queries are executed by PHP. This tight integration involves the PHP process being closely linked to Apache for high performance. PHP can be thought of as the middle ground for accessing databases, files, XML, and so on, and this middle ground sends everything out of the machine via Apache. MySQL should be thought of purely as a data storage device that is useful only when something else connects to it to add, remove, update, or request information. You can consider MySQL as the equivalent of a hard disk for a computer; a hard disk is useful only if there is software to access it and store data on it. PHP is the metaphorical equivalent to this "software."

## SUMMARY

As with learning anything, PHP and MySQL development has a number of underlying concepts that need to be understood before you hit the nitty-gritty of the subject. The major concepts have been discussed in this chapter to provide a solid foundation.

The next chapter moves on and teaches the core principles of PHP and MySQL. You will discover the fundamental language bits and pieces, and then get straight to writing an application. With each application, you will explore new concepts and skills, and push your knowledge further, while always writing relevant Web applications.

*This page intentionally left blank*

## Getting Started with PHP and MySQL

As the proud owner of Practical PHP and MySQL or a prospective owner rifling through it in a bookstore—you will be pleased to know that this book consists of a number of real-world Web applications that are built from scratch. Although the main focus of the book is to teach you how to create these applications, it is important to review some of the introductory aspects of learning PHP and MySQL. This chapter provides a quick primer.

The intention of this chapter is not to be exhaustive, but to provide a solid introduction to PHP and MySQL—enough to get you started writing applications. Many PHP and MySQL books spend most of the time discussing abstract concepts that don't relate in any way, and you can often see the eyes of the readers physically glazing over with sheer, unadulterated boredom. As a man who objects to any kind of retina glazing, you won't find this kind of content here. The grand plan is to show you enough of PHP and MySQL to get started and then get on with the interesting stuff: writing applications.

This chapter discusses core PHP language fundamentals such as loops and variables and then moves on to cover how to create a database and access it from PHP. The chapter concludes with coverage of sessions, a key technology used in most Web applications. Although this chapter provides an introduction to these concepts, the real action happens inside the applications you will write. Each project provides a means to explore further into the many aspects of programming PHP and MySQL Web applications, and the general ethos is of learning by doing instead of learning by reading.

16 Practical PHP and MySQL

## Setting up PHP and MySQL

When I started teaching people how to use PHP and MySQL, I would typically teach it within the safe confines of a computer lab, complete with a network of perfectly set up and configured machines. My students would come to the course, learn how to use the software, and leave incredibly excited about the potential that PHP and MySQL gave them. Then, a few days later, I would start getting e-mails detailing problems they were facing when installing PHP, MySQL, and Apache on Windows, Linux, or Mac OS X. Although the computer lab was great for teaching the software, the course back then did not cover installation—yet it was evidently such a hurdle.

The problem is that PHP, Apache, and MySQL are really difficult to set up on Windows. They are much easier to set up on Linux because the major distributions typically include MySQL, Apache, and PHP packages, but on Windows it is a royal pain in the nether region. Back then, I was somewhat stumped about what to do—teaching the installation side of the software could take up a substantial amount of time on the course.

Then, in a fit of pure genius, my colleague and friend Elliot Smith discovered XAMPP (www.xampp.org/). XAMPP provides a complete PHP, Apache, and MySQL (web development environment that can be installed by downloading, unzipping, and running the software. XAMPP makes the installation dramatically easier, and the software also includes a raft of additions and extras that are genuinely useful, including PHP extensions, a Web front-end for MySQL (which is used throughout the book), and more. XAMPP is freely available for Windows, Linux, Mac OS X, and Solaris.

It is recommended that you use XAMPP for setting up the software if you have never done it before. The following sections cover how to set up XAMPP on Windows and Linux.

### Setting Up XAMPP on Windows

To begin, download the latest XAMPP installer from www.xampp.org/. Double-click the installer and follow the instructions. After installation, load the XAMPP Control Panel by clicking Start > Programs > XAMPP.

### Setting Up XAMPP on Linux

To begin, download the latest XAMPP release from www.xampp.org/. Next, copy the installation file to /opt and then unzip it. If you don't have an /opt directory, create it with 'mkdir /opt' as the superuser. If you don't have sudo installed on your computer, you can become the superuser by running 'su' and entering your superuser password.

To copy the file to /opt:

```
foo@bar:~$ sudo cp xampp-linux-x.x-x.tar.gz /opt
```

To move to /opt and unzip the file:

```
foo@bar:~$ cd /opt
foo@bar:/opt$ sudo tar zxvf xampp-linux-x.x-x.tar.gz /opt
```

A stream of files is now unpacked into a directory called **lampp**. Currently, all of this unpacking has been done as the superuser, yet you will want your normal user account to be able to write to the **htdocs** directory, so change the permissions on the directory:

```
foo@bar:/opt$ sudo chmod -R a+rw /opt/lampp/htdocs
```

You are now all set to run XAMPP:

```
foo@bar:/opt$ sudo /opt/lampp/lampp start
```

You can also stop XAMPP:

```
foo@bar:/opt$ sudo /opt/lampp/lampp stop
```

You can now save your PHP code in /opt/lampp/htdocs and access your new XAMPP server in your Web browser at http://localhost/.

### NOTE

### XAMPP Control Panel for Linux

Rather disappointed with the nice graphical XAMPP Control Panel for Windows, I wrote one in Python for Linux, and it is now included with the official XAMPP release. You can find it in /opt/lampp/share/xampp-control-panel. Just run it like this:

```
foo@bar:/opt/lampp/share/xampp-control-panel$ sudo ./xampp-control-panel
```

## GETTING STARTED WITH PHP

PHP and HTML are good friends. Working side by side, the PHP and HTML pals are so reliant on each other that it is virtually impossible to tear them apart. Whenever you do any kind of Web development, you use PHP and HTML
