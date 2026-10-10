386  **Appendix: Self Test**

# CHAPTER 5: CONFIGURING THE BASE SYSTEM

+   1. Your manager wants you to change the system prompt for users on their system to reflect that the company has merged with another company and has rebranded itself as Plix. The manger wants users to have the prompt as `"plix>"` (without the `"` marks). What is the correct method to undertake this?
+   
+      - **A.** Put the following in the /usr/local/bashrc file `PS2=\"plix>\"`
+      - **B.** Put the following in the /usr/profile file `PS1=\"plix>\"`
+      - **C.** Add the following to the `~/.bashrc` file for each user `PS1=\"plix>\"`
+      - **D.** Insert the following into `/etc/env` file `PS1=\"plix>\"`
+   
+      Correct answer and explanation: **C.** Answer **C** is correct as this will display the prompt for the users. Users can also change this prompt to their own setting if they wish to do so later.
+   
+      Incorrect answers and explanations: **A, B, and D.** Answers **A, B, and D** are incorrect as the configuration file mentioned do not exist in that directory and is not read by the system.

+   2. You wish to run a program called `disp_rights` you have developed and placed in your home directory. You have limited its rights so that it can only be executed by yourself. Your username is `syngress`. Which command will execute the program?
+   
+      - **A.** `syngress/disp_rights`
+      - **B.** `~/disp_rights`
+      - **C.** `~/syngress/disp_rights`
+      - **D.** `/usr/home/syngress/disp_rights`
+   
+      Correct answer and explanation: **B.** Answer **B** is correct as the `~` symbol specifies your home directory.
+   
+      Incorrect answers and explanations: **A, C, and D.** Answer **A** is incorrect as `syngress` is the incorrect notation for your home directory. Answer **C** is incorrect as this specifies a subdirectory called `syngress` off your home directory. Answer **D** is incorrect as this does not specify where your home directory is.

+   3. You wish to find the default mail server for the domain `mycorp.com`. Using the `dig` command, you display the information currently held in the DNS server. Which of the resource record types below correctly defines the mail server's IP address?
+   
+      - **A.** NS
+      - **B.** A