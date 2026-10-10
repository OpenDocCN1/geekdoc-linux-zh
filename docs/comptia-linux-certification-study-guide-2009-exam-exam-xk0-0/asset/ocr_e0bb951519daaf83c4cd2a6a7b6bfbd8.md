command had been `tar czvf work.tgz /home`, then this would have restored them to the original location.

Incorrect answers and explanations: **A, B**, and **D**. Answer **A** is incorrect as the files were archived with a relative and not absolute location. Answer **B** is wrong as the files are restored relative to where you are (/tmp/). Answer **D** is wrong as the option o is invalid.

**9.** You are installing a number of new packages to an older machine that does not have a large amount of disk space and you do not want to install any documentation on the packages as you can look at this on another machine. What option should you add to rpm to ensure this happens?

+   * **A.** Include the option `--minimize`
+   * **B.** Include the option `--excludedocs`
+   * **C.** Include the option `--excludedocumentation`
+   * **D.** Include the option `--nodocsc`

Correct answer and explanation: **B**. Answer **B** is correct as this is the right option to install the software without any supporting documentation.

Incorrect answers and explanations: **A, C**, and **D**. Answer **A** is incorrect as there is no `minimize` option. Answer **C** is incorrect as the option is `excludedocs` and not `excludedocumentation`. Answer **D** is incorrect as there is no `nodocsc` option in rpm.

**10.** You have downloaded the source code for a new Web program into /tmp and have read the INSTALL file that came with it. The INSTALL file says you have to run the command:

```
./configure --prefix=targetdirectory
```

Where do you think the makefile will be created?

+   * **A.** In the current directory
+   * **B.** In a subdirectory called targetdirectory from the current directory
+   * **C.** In a directory called targetdirectory in your home directory
+   * **D.** Nowhere as the makefile is created by make

Correct answer and explanation: **B**. Answer **B** is correct as the option `--prefix` will change the path where the *makefile* is created.

Incorrect answers and explanations: **A, C**, and **D**. Answer **A** is incorrect as this is the normal location of the *makefile*, but it is overridden by the prefix option. Answer **C** is incorrect as the *makefile* would be created here if you located the source files here or added the path into the prefix option. Answer **D** is incorrect as `make` uses the *makefile* produced by configuration.