Answer **a** is correct. Solaris 8 cannot be installed on a Macintosh system. Solaris 8 can be installed on Sun SPARC, Intel Pentium, or Intel-compatibles (AMD and Cyrix). Therefore, answers **b**, **c**, and **d** are incorrect.

# Question 6

+   Which of the following commands displays selected information from the SUNWast pkginfo file? (Select all that apply.)
+   
+   - [ ] a. `pkginfo SUNWast`
+   - [ ] b. `pkginfo -l SUNWast`
+   - [ ] c. `display pkginfo SUNWast`
+   - [ ] d. Highlight SUNWast in the Admintool: Software dialog box and click Show Details.

Answers **a**, **b**, and **d** are correct. You can display selected information from the SUNWast pkginfo file by using the `pkginfo SUNWast` or `pkginfo -l SUNWast` command, or by highlighting SUNWast in the Admintool: Software dialog box and clicking Show Details. Although the command in answer **a** provides only the package title and type of software, the pkginfo file is the only place you can obtain this information. The command in answer **c** does not exist.

# Question 7

+   Which of the following commands can be used to remove a patch?
+   
+   - ( ) a. `rmpatch`
+   - ( ) b. `patchrm`
+   - ( ) c. `pkgrm -p`
+   - ( ) d. `patchadd -d`

Answer **b** is correct. You can use the `patchrm` command to remove a patch. Answer **a** (`rmpatch`) is not a valid command. The `pkgrm` command is used to remove packages, and no `-p` command-line argument exists. Therefore, answer **c** is incorrect. The `patchadd -d` command is used to add a patch without saving files before they are updated or replaced. Therefore, answer **d** is incorrect.