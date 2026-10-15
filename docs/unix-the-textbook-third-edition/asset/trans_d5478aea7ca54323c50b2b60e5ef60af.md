

# 表 17.3 git 命令

| Command | Description |
|---|---|
| git init | Add a Git repository in the current directory |
| git add <file> | Stage <file> for the next commit |
| git commit -m "Message" | Execute a commit with Message automatically added using the -m option. |
| git remote add origin <path> | Identify the valid <path> as a Git remote repository reference |
| git push -u origin master | Transmit the branch named master to the current remote repository and add upstream tracking information |
| git remote -v | List the remotes defined for this repository |

Prerequisites: The following are the prerequisites for carrying out this example:

- 1. Having an account on GitHub and knowing how to add a new repository to that account
- 2. Having completed the previous subsections that familiarize you with Git commands executed on the UNIX command line
- 3. Having an Internet connection and a suitable Web browser installed and operating on your UNIX system
- 4. Local and remote GitHub repositories with only one branch each
- 5. Having completed Example 17.2

Procedure: Do the following steps, in the order presented, to meet the objectives of this example.

- 1. Create the working directory and make it the current directory.
  % mkdir githubtest
  % cd githubtest
  %

- 2. Add a new file to the directory.
  % touch README.md
  %

- 3. Initialize Git in this new directory.
  % git init
  Initialized empty Git repository in /usr/home/bob/githubtest/.git/
  %

- 4. Stage the file README.md, and do an initial commit to the repository.
  % git add README.md
  % git commit -m "First Commit"
  [master (root-commit) f971bid] First Commit
  1 file changed, 0 insertions(+), 0 deletions(-)
  create mode 100644 README.md
  %

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

```
newfile.txt: new file: 1 lines, 47 characters.
%
```

## 11. List the files in your working directory.

```
% ls
README.md newfile.txt
%
```

## 12. Stage newfile.txt and commit it.

```
% git add newfile.txt
% git commit -m "second new file added"
[master 4dc2de7] second new file added
1 file changed, 1 insertion(+)
create mode 100644 newfile.txt
%
```

## 13. Now use git push again to push the contents of the repository to your GitHub repository.

```
% git push origin master
Username for 'https://github.com/': bobk48
Password for 'https://bobk48@gmail.com@github.com/': xxx
Counting objects: 4, done.
Delta compression using up to 2 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 325 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/bobk48/test.git
f971bid..4dc2de7 master -> master
%
```

In your browser, check the content of your GitHub repository named test. You should see the same files there that are in your local repository along the branch master.

> Conclusions: By designating a GitHub repository as a remote repository reference using an https URL, we accomplished moving files up from a local repository to a GitHub repository.

# 练习 17.15

What refspec URL and fetch assignments are listed for the repository test? What branch refspecs are listed? How did you find this out?

# 练习 17.16

What Git command do you use locally to put an earlier, or upstream, commit into the working directory?

