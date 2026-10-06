# Chapter 9 • Writing Scripts, Configuring Email, and Using Databases

5. Which of the following commands, if typed in a bash shell, will create an environment variable MYVAR with the contents myststuff that will be accessible to subsequently launched programs?

+   A. export MYVAR='myststuff'
B. MYVAR='myststuff'
C. $MYVAR==myststuff
D. echo $MYVAR myststuff
E. setenv MYVAR myststuff

6. What file might a user modify to alter or her own bash environment?

+   A. ~/.startup
B. /etc/bashrc
C. /home/.bashrc
D. /home/.profilerc
E. ~/.bashrc

7. What commands might you use (along with appropriate options) to learn the value of a specific environment variable? (Select two.)

+   A. env
B. DISPLAY
C. export
D. echo
E. cat

8. After using a text editor to create a shell script, what step should you take before trying to use the script?

+   A. Set the UID bit using chmod.
B. Copy the script to the /usr/bin/scripts directory.
C. Compile the script by typing scriptname, where scriptname is the script's name.
D. Run a virus checker on the script to be sure it contains no viruses.
E. Set one or more executable bits using chmod.

9. Describe the effect of the following short script, cp1, if it's called as cp1 big.c big.cc:
!/bin/bash
cp $2 $1

+   A. It has the same effect as the cp command—copying the contents of big.c to big.cc.
B. It compiles the C program big.c and calls the result big.cc.
C. It copies the contents of big.c to big.cc, eliminating the old big.c.
D. It converts the C program big.c into a C++ program big.cc.
E. It interprets the big.c and big.cc files as bash scripts.