5. In your Web browser, navigate to GitHub at www.github.com, log in, and create a new repository in your GitHub account. Name that repository test.

6. Use the git remote command to designate your GitHub repository test as a remote repository for the local repository we created in steps 1-4. To find the URL to designate as the GitHub repository, look in the URL bar of your browser when you are in the GitHub repository named test that you created in step 5. On our system, in our browser, the URL to this new repository on GitHub is https://github.com/bobk48/test.git

```
% git remote add origin https://github.com/bobk48/test.git
%
```

7. Use the git push command to take the local repository and move it up to GitHub. Supply the username and password for the GitHub repository as needed.

```
% git push -u origin master
Username for 'https://github.com': bobk48
Password for 'https://bobk48@github.com': xxx
Counting objects: 3, done.
Writing objects: 100% (3/3), 207 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/bobk48/test.git
 * [new branch]      master -> master
Branch master set up to track remote branch master from origin.
%
```

8. Check the names of the files in the local repository.

```
% ls
README.md
%
```

In your browser, check the content of the repository test.

9. Use the git remote command to list the remote repositories for this local repository.

```
% git remote -v
origin https://github.com/bobk48/test.git (fetch)
origin https://github.com/bobk48/test.git (push)
%
```

What this output shows you is that you can transfer (using the git push command) new content to the remote repository, and get content from it (using the git fetch command).

10. To add a new file to the GitHub repository from the local repository, first create the file with your favorite text editor.

```
% vi newfile.txt
... Create and save a new textfile named newfile.txt ...
```