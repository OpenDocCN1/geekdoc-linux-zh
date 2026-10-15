Procedure: Perform the following steps, in the order presented, to meet the objectives of this example:

+   1. Create a new empty directory beneath your home directory on your UNIX system named github_clone and make that directory the current working directory.
+   ```
+   % mkdir github_clone
+   % cd github_clone
+   %
+   ```
+   This new directory will serve as the file system landing zone, within which the git clone command shown in the next step will replicate the entire remote GitHub repository.

+   2. Use the git clone command to transfer the contents of the remote GitHub repository into the current working directory. Remember that the URL we show in the command is different from the one that you will be seeing on your system, so make the appropriate changes.
+   ```
+   % git clone https://github.com/bobk48/test
+   Cloning into 'test'...
+   remote: Counting objects: 6, done.
+   remote: Compressing objects: 100% (3/3), done.
+   remote: Total 6 (delta 0), reused 6 (delta 0)
+   Receiving objects: 100% (6/6), done.
+   Checking connectivity... done.
+   %
+   ```

+   3. List the contents of the working directory. It should contain the complete repository from your GitHub repository in Example 17.3. The directory listed is the working directory for the cloned repository. If you descend into that directory, everything that is in your GitHub repository is in test.
+   ```
+   % ls
+   test
+   %
+   ```

+   4. Make the directory test the current directory, in preparation for putting a new file in it that you will then transfer up to the GitHub repository.
+   ```
+   % cd test
+   %
+   ```
+   The test directory is now your working directory in Git terminology.

+   5. With your favorite text editor, create a new file, with any contents you want in it, in the directory test. Save the file and exit the text editor.
+   ```
+   % vi newfile2.txt
+   newfile2.txt: new file: 1 lines, 58 characters.
+   %
+   ```