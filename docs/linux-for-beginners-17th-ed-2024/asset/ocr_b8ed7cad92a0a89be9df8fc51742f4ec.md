# Creating and Removing Directories

As with creating files in the Terminal, you can also create and delete directories, or folders if you prefer. Directories form the structure of your file system, without logical directories the filing system would be in utter chaos.

# MANAGING FOLDERS

Learning how to create and delete folders in the Terminal is an important Mint, and indeed Linux overall, skill to master. Here's the basics for you to try out.

+   **STEP 1**  With the Terminal open enter `cd` – to make sure you’re in your own Home directory. Now enter `ls` to view the current folders you have housed in the Home directory. You’ll notice that folders are labelled in Mint in cyan (light blue). Let’s start by creating a new directory. Enter `mkdir testdir`.

![](bbox=[0.07, 0.5, 0.49, 0.66])

+   **STEP 3** If you were to enter the command again, `mkdir testdir`, you’ll receive a message stating: `mkdir: cannot create directory ‘testdir’: File exists`. It goes without saying then, that you’re only able to have one uniquely named directory within the current directory. However, as Linux is case-sensitive, you can have `TestDir`, `TesDir`, `testDir` and so on.

![](bbox=[0.51, 0.5, 0.93, 0.66])

+   **STEP 2** If you now enter `ls` again, you’ll see that the new directory, testdir, has been created alongside the other directories in the Home area. Obviously the command `mkdir` is what creates the directory, and no doubt you’ve already guessed it stands for Make Directory.

+   **STEP 4** You can create directories within directories you’ve already created. For example, enter the testdir directory with `cd testdir/`, followed by `ls` to list the folder structure. Naturally there’s nothing present, as you’ve just created the directory.
+   
+   Now drop back to Home with `cd ~`, and enter `mkdir testdir/reports`. Go back to the testdir, `cd testdir/`, and `ls` again.

![](bbox=[0.07, 0.75, 0.49, 0.94])

![](bbox=[0.51, 0.77, 0.93, 0.94])

58

www.mymagbooks.com  mymag.com.au/mymag