> the `.git/COMMIT_EDITMSG` file by hand. The vim editor was covered in Chapter 10, “Working with Editors.”

Now that the script project is committed to the local repository, it can be shared with other script project team members by pushing it to the remote repository. If the script(s) is completed, you can also share it with select others or the whole world.

If this is a new script project, after the remote repository account is established, create a special file called a *Markdown file*. The file's content displays on the remote repository's web page and describes the repository. It uses what is called *Markdown* language. You'll need to name the file **README.md**. Here is an example of creating this file, adding it to the staging area index, and committing it to the local repository:

```
$ pwd
/home/christine/MwGuard
$
$ ls
MyGitExampleScript.sh
$
$ echo "# Milky Way Guardian" > README.md
$ echo "## Script Project" >> README.md
$
$ cat README.md
# Milky Way Guardian
## Script Project
$
$
$ git add README.md
$
$ git status
[...]
Changes to be committed:
   (use "git restore --staged <file>..." to unstage)
  new file:   README.md


$ git commit -m "README.md commit"
[...]
README.md commit
1 file changed, 2 insertions(+)
create mode 100644 README.md
$
```