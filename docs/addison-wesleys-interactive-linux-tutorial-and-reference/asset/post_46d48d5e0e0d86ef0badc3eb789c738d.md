
# Module 13 Find, Copy, and Move with vi

1. Change to your directory *practice*.
   - a. Type `cd $HOME/practice`
   - b. Press `<Enter>`

2. Open *vi* with the file *nowtime*.
   - a. Type `vi nowtime`
   - b. Press `<Enter>`

4. In this exercise, you will search for "is".
   - a. Press `<G>`
   - b. Press `<$>`

5. In this exercise, you will search for "right."
   - a. Press `<1G>`

6. In this exercise, you will use `<yws>` to copy a small word forward.
   - a. Press `<1G>`
   - b. Press `<u>`

8. In this exercise, you will use `<y2>` to yank two sentences forward.
   - a. Press `<0>`
   - b. Press `<3k>`
   - c. Press `<G>`
   - d. Press `<o>`

9. In this exercise, you will use `<y2l>` to yank two paragraphs forward.
   - c. Press `<Ctrl-I>`
   - d. Press `<G>`
   - f. Press `<u>`

10. In this exercise, you will use *put* to insert text after using a delete command.
   - b. Press `<$>`
   - d. Press `<0>`
   - e. Press `<3j>`
   - h. Press `<2h>` or press `<h>` twice.
   - i. Insert a space between "time" and "yet."
     - (1) Press `<i>`
     - (2) Press the `<Space Bar>`
     - (3) Press `<Esc>`

11. In this exercise, you will yank an entire line with `<yy>`.
   - a. Move the cursor up one line.
     - (1) Press <`^K`>
   - c. Move the cursor to the top of the file.
     - (1) Press <`^G`>
   - d. Create a blank line above the first line.
     - (1) Press <`^O`>
     - (2) Press <`Esc`>

12. Quit `vi` without saving the file.
   - a. Type <`^D^D`>
   - b. Press <`Enter`>

# Module 14 `vi` Advanced Commands

1. Change to your directory **practice**.
   - a. Type `cd $HOME/practice`
   - b. Press <`Enter`>

2. Open `vi` to create a new file named **one-nine**.
   - a. Type `vi one-nine`
   - b. Press <`Enter`>

3. Create the file **one-nine**. Your screen should look like Figure 14-1. When you have finished creating the file, save it.
   - a. Press <`i`> to put `vi` in input mode.
   - b. Type **One.** (Note the period at the end.)
   - c. Press <`Enter`>
   - d. Type **Two.**
   - e. Press <`Enter`>
   - f. Type **Three.**
   - g. Press <`Enter`>
   - h. Type **Four.**
   - i. Press <`Enter`>
   - j. Type **Five.**
   - k. Press <Enter>
   - l. Type **Six.**
   - m. Press <Enter>
   - n. Type **Seven.**
   - o. Press <Enter>
   - p. Type **Eight.**
   - q. Press <Enter>
   - r. Type **Nine.**
   - s. Press <Esc>
   - t. Press <w>
   - u. Press <Enter>

6. In this exercise, you will cycle through the numbered buffers.
   - a. Press <j>
   - b. Create two blank lines below the current line.
     - (1) Press <o>
     - (2) Press <Enter>
     - (3) Press <Esc>

9. In this exercise, you will create the file pressrel.text.
   - e. (1) Press <i> to put vi in input mode.
     - (2) Type:
       > Robert Johnsons, VP NASR Sales, has announced the formation of a company task force whose goal will be to evaluate the utilization of telecommunication resources. AA Named to the task force today were:
     - (3) Press <Esc> to get out of input mode and return to command mode.

10. In this exercise, you will create the file members1.text.
   - e. Enter the following text. Each name should be on a separate line:
     - (1) Press <i> to put vi in input mode.
     - (2) Type **Samantha Innick**

![](img/cc8b9fd5970716027fba0d0a45c13900_322_0.png)

   - (3) Press <Enter>
   - (4) Type **Samuel Stephens**
   - (5) Press <Enter>
   - (6) Type **Andrew Thomas**
   - (7) Press <Esc>
   - f. Save the file.
     - (1) Press <w>
     - (2) Press <Enter>

11. In this exercise, you will create the file **members2.text**.
   - e. Enter the following text. Each name should be on a separate line:
     - (1) Press <i> to put vi in input mode.
     - (2) Type **Charles Denton**
     - (3) Press <Enter>
     - (4) Type **Wendy Franks**
     - (5) Press <Enter>
     - (6) Type **Roberta Johnson**
     - (7) Press <Esc>
   - f. Save the file.
     - (1) Press <w>
     - (2) Press <Enter>

12. In this exercise, you will check the spelling of the names on the two personnel lists.
   - a. You think Wendy's last name is spelled “Franks.” Change the spelling to “Frankes.”
     - (1) Press <k>
     - (2) Press <i> to put vi in input mode.
     - (3) Type **e**
     - (4) Press <Esc>
   - b. On further reflection, you decide that the original spelling was correct. Delete the “e.”
     - (1) Press <x> to delete the “e.”

**Try It Live! Answer Key**

204

13. In this exercise, you will place the contents of both members’ files in named buffers.
   - d. Make certain that the cursor is on the first character of the file.
     - (1) Press <1G>

14. In this exercise, you will open the file pressrel.text and put the contents of named buffer “a”.
   - c. Move the cursor to the bottom line of the file.
     - (1) Press <G>

15. In this exercise, you will add the contents of named buffer “b” to pressrel.text.
   - b. Undo the put.
     - (1) Press <u>

16. Move “Samantha Innick” to a separate line.
   - a. Press <2j> so that your cursor is on the line “Roberta JohnsonSamantha Innick”.
   - b. Press <w>
   - c. Press <l> to move the cursor to the “S” of “Samantha”.
   - d. Press <i>
   - e. Press <Enter>
   - f. Press <Esc>

17. Save the file, and quit vi.
   - a. Press <wq>
   - b. Press <Enter>

![](img/cc8b9fd5970716027fba0d0a45c13900_324_0.png)

# Linux Made Easy CBT Software End User License Agreement

This software license agreement ("License") is an agreement between you and Edutrends, Inc. (Edutrends). Edutrends is willing to license the enclosed software to you only upon the condition that you accept all of the terms contained in this license. Please read this license carefully before installing, copying, downloading, accessing or otherwise using the software, as by using the software you indicate that you agree to be bound by the terms of this license. If you do not agree to the terms of this license, Edutrends is unwilling to license the software to you, and you should promptly return the unused software to the place where you obtained it and your money will be refunded.

**1. Grant of License.**

The software accompanying this License, whether on CD-ROM, diskette or any other media (the "Software") and the related documentation are licensed to you by Edutrends according to the terms of the License. This License allows you to use the Software on a single computer. You may also use a copy of the Software on a home or portable computer, as long as that extra copy is never running at the same time the Software is running on the primary computer on which you use the Software.

You may make one additional copy of the Software in the form in which it is provided to you, only for backup purposes. You must reproduce on all copies you make of the Software the copyright notice and any other proprietary legends that are on the original copy of the Software. You may also transfer to another party all your license rights in the Software and related documentation by transferring to that party both the original media on which the Software and related documentation were provided and a copy of this License, provided that the other party reads and agrees to accept the terms and conditions of this License. Immediately upon transfer, you have no further rights to use or own copies of the Software or related documentation and must destroy all copies in your possession or control.

If you purchased the enhanced educational version of Linux Made Easy, which is part of an Addison Wesley book/CD package, you are granted a one year license to use this computer based training software, commencing with the date you install the software on your computer.

**2. Restrictions.**

The Software contains copyrighted material, trade secrets, and other proprietary material of Edutrends, Delphi Inc. (Delphi) and/or its licensors. You agree that in order to protect those proprietary materials, you will not decompile, reverse engineer, disassemble or otherwise reduce all or any part of the Software to human-readable form. You may not modify, rent, lease, loan, distribute or create derivative works based upon the Software in whole or in part. If the Software is labeled as an educational version or is otherwise licensed to you for academic use, you must be a student, faculty or staff of an educational institution.

**3. Ownership.**

The Software and documentation are licensed, not sold, to you for use only under the terms of this License, and Edutrends and Delphi reserve all rights not expressly granted to you in this License. All title, intellectual property rights and copyrights in and to the Software, the accompanying printed materials, and any copies of the software materials, are owned by Edutrends, Delphi and/or its suppliers.
