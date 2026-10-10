Correct answer and explanation: **D**. Answer **D** is correct because `apt-get update` performs an update of the APT database but does not upgrade any of the installed applications themselves. Furthermore, the syntax is incorrect because a package name is not used with `apt-get update`.

Incorrect answers and explanations: **A**, **B**, and **C**. Answers **A**, **B**, and **C** are incorrect because all these three commands can be used to install or upgrade an installed .deb package.

+   14.  You are compiling source code for installation and you want to string
+       all of the required commands together to run while you are going
+       downstairs to grab a coffee so that the binary file is ready when you
+       return. What answer below has syntax that will not work?

+   A.  `./configure; make; make install`
+   B.  `./configure / make / make install`
+   C.  `./configure && make && make install`
+   D.  `./configure | make | make install`

Correct answer and explanation: **B**. Answer **B** is correct. The fore slash is not a valid character for use in concatenating commands. It is used in denoting filesystem locations, such as the root directory, `"/"`.

Incorrect answers and explanations: **A**, **C**, and **D**. The semicolon and the double ampersands have a similar function; they simply concatenate the commands. The first command executes and once it terminates, the second command executes, and so on. The pipe command, `"|"`, sends the output of the first command as input into the second command. Please refer to Chapter 6 for information on scripting and output redirection.

+   15.  You are powering up a laptop that has Linux installed that has not
+       been used in a couple of months. Since you will be handing it over to
+       a user who needs to use it on a long trip, you want to ensure that its
+       applications are current. What command do you run once the APT
+       database is up-to-date?

+   A.  `apt-get update`
+   B.  `apt-get upgrade`
+   C.  `apt-get dist-upgrade`
+   D.  `apt-get install`

Correct answer and explanation: **B**. Answer **B** is correct because `apt-get upgrade` uses the information in the APT database,