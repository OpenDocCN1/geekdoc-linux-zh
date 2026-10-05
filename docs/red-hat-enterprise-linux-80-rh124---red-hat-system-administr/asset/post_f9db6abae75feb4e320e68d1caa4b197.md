
-   Create a hard link named /home/student/hardlink to the file /home/student/grading/grade1. You will need to do this after creating the empty file /home/student/grading/grade3 as specified above.
-   Create a soft link named /home/student/softlink to the file /home/student/grading/grade2.
-   Save the output of a command that lists the contents of the /boot directory to the file /home/student/grading/longlisting.txt. The output should be a "long listing" that includes file permissions, owner and group owner, size, and modification date of each file.

# Evaluation

On workstation, run the lab rhcsa-rh124-review1 grade command to confirm success of this exercise.

```bash
[student@workstation ~]$ lab rhcsa-rh124-review1 grade
```

# Finish

On workstation, run lab rhcsa-rh124-review1 finish to complete the comprehensive review. This script deletes the files and directories created during the start of the comprehensive review and ensures that the environment on serverb is clean.

```bash
[student@workstation ~]$ lab rhcsa-rh124-review1 finish
```

This concludes the comprehensive review.

# SOLUTION

# MANAGING FILES FROM THE COMMAND LINE

In this review, you will manage files, redirect a specific set of lines from a text file to another file and edit the files.

# OUTCOMES

You should be able to:
-   Manage files from the command line.
-   Display a certain number of lines from files and redirect the output to another file.
-   Edit files.

# BEFORE YOU BEGIN

Log in to workstation as student using the password. On workstation, run lab rhcsa-rh124-review1 start to start the comprehensive review. This script creates the necessary files to set up the environment correctly.

```bash
[student@workstation ~]$ lab rhcsa-rh124-review1 start
```

# INSTRUCTIONS

Accomplish the following tasks on serverb to complete the exercise:

-   Create a new directory named /home/student/grading.
-   Create three empty files in the /home/student/grading directory named grade1, grade2, and grade3.
-   Capture the first five lines of the /home/student/grading/manage-files file in /home/student/grading/manage-files.txt.
-   Append the last three lines of /home/student/grading/manage-files to the file /home/student/grading/manage-files.txt. You must not overwrite any text already in the file /home/student/grading/manage-files.txt.
-   Copy /home/student/grading/manage-files.txt to /home/student/grading/manage-files-copy.txt.
-   Edit the file /home/student/grading/manage-files-copy.txt so that there should be two sequential lines of text JJ.
-   Edit the file /home/student/grading/manage-files-copy.txt so that the HH line must not exist in the file.
-   Edit the file /home/student/grading/manage-files-copy.txt so that a new line should exist between CC.

-   Create a hard link named /home/student/hardlink to the file /home/student/grading/grade1. You will need to do this after creating the empty file /home/student/grading/grade3 as specified above.
-   Create a soft link named /home/student/softlink to the file /home/student/grading/grade2.
-   Save the output of a command that lists the contents of the /boot directory to the file /home/student/grading/longlisting.txt. The output should be a "long listing" that includes file permissions, owner and group owner, size, and modification date of each file.

-   1. Create a new directory called /home/student/grading.
    1.1 From workstation, open an SSH session to serverb as student.
    ```bash
    [student@workstation ~]$ ssh student@serverb
    [student@serverb ~]$
    ```
    1.2 Use the mkdir command to create the /home/student/grading directory.
    ```bash
    [student@serverb ~]$ mkdir grading
    ```
    As you ran the preceding command in the home directory of the student user, you did not specify the absolute path to the grading directory while creating it.

-   2. Create three empty files in the /home/student/grading directory named grade1, grade2, and grade3.
    2.1 Use the touch command to create the empty files grade1, grade2, and grade3 in the /home/student/grading directory. Apply the brace expansion feature to create all three files with a single command.
    ```bash
    [student@serverb ~]$ touch grading/{1,2,3}
    ```
    2.2 Use the ls command to verify that the grade1, grade2, and grade3 files exist under the directory /home/student/grading.
    ```bash
    [student@serverb ~]$ ls grading/
    grade1 grade2 grade3
    ```

-   3. Capture the first five lines of the /home/student/grading/manage-files file in /home/student/grading/manage-files.txt.
    3.1 Use the head command to view the first five lines of the file /home/student/grading/manage-files and redirect the output to the file /home/student/grading/manage-files.txt.
    ```bash
    [student@serverb ~]$ head -5 manage-files > grading/manage-files.txt
    ```
    The preceding command uses the redirection symbol (>) to save the command output to /home/student/grading/manage-files.txt so that any existing content in the file gets overwritten.
    3.2 Verify that the file /home/student/grading/manage-files.txt contains the following text:
    ```
    Test AA
    Test BB
    Test CC
    Test DD
    Test EE
    ```

-   4. Append the last three lines of /home/student/grading/manage-files to the file /home/student/grading/manage-files.txt. You must not overwrite any text already in the file /home/student/grading/manage-files.txt.
    4.1 Use the tail command to view the last three lines of the file /home/student/grading/manage-files and append the output to /home/student/grading/manage-files.txt.
    ```bash
    [student@serverb ~]$ tail -3 manage-files >> grading/manage-files.txt
    ```
    The preceding command uses the double redirection symbol (>>) to append the output to /home/student/grading/manage-files.txt so that the existing contents in the file are preserved.
    4.2. Verify that the file /home/student/grading/manage-files.txt contains the following text:
    ```
    Test AA
    Test BB
    Test CC
    Test DD
    Test HH
    Test II
    Test JJ
    ```

-   5. Copy the /home/student/grading/manage-files.txt file to /home/student/grading/manage-files-copy.txt.
    5.1 Use the cd command to navigate to the directory /home/student/grading.
    ```bash
    [student@serverb ~]$ cd grading/
    ```

# CRITERIA | Comprehensive review

5.2 Use the cp command to copy the /home/student/grading/manage-files.txt file to /home/student/grading/manage-files-copy.txt.
    ```bash
    [student@serverb grading]$ cp manage-files.txt manage-files-copy.txt
    ```
    5.3 Navigate to the home directory of the user student.
    ```bash
    [student@serverb grading]$ cd
    [student@serverb ~]$
    ```

-   6. Edit the file /home/student/grading/manage-files-copy.txt so that there should be two sequential lines of text JJ.
    6.1 Use the vim editor to open the /home/student/grading/manage-files-copy.txt file.
    ```bash
    [student@serverb ~]$ vim grading/manage-files-copy.txt
    ```
    6.2 From the command mode in vim, scroll down to the line that has the Test JJ line of text. Press the y key on your keyboard to copy the line of text and press the p key to paste it below the cursor. :wq to save the changes and exit vim. Verify that the /home/student/grading/manage-files-copy.txt file contains the text:
    ```
    Test AA
    Test BB
    Test CC
    Test DD
    Test EE
    Test HH
    Test II
    Test JJ
    Test JJ
    ```
    Notice that the preceding content includes two copies of the Test JJ line of text.
    Edit the file /home/student/grading/manage-files-copy.txt so that the HH line of text must not exist in the file.
    7.1 Use the vim editor to open the /home/student/grading/manage-files-copy.txt file.
    ```bash
    [student@serverb ~]$ vim grading/manage-files-copy.txt
    ```
    7.2. From the command mode in vim, scroll down to the line that has the Test HH line of text. Press the d key on your keyboard to delete the line of text. Type :wq to save the changes and quit vim. Verify that the /home/student/grading/manage-files-copy.txt file contains the following text.
