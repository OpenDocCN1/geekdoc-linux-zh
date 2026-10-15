To avoid these stumbling blocks, run **git status** and assess the situation manually. This command informs you of new files, modified files, and staged files all at once. For example, suppose that we edited **/etc/mdadm/mdadm.conf** as in the previous example and also installed a new system daemon, **foobar**, whose configuration file is **/etc/foobar/foobar.conf**. Git might show the following:

```
$ sudo git status
# On branch master
# Changed but not updated:
#   (use "git add <file>..." to update what will be committed)
#
#       modified:   mdadm/mdadm.conf
#       modified:   mtab
#       modified:   passwd
#
# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#
#       foobar/
no changes added to commit (use "git add" and/or "git commit -a")
```

The **foobar.conf** file is not listed by name because Git doesn’t yet see beneath the **foobar** directory that contains it. We can see that both **mtab** and **passwd** have unexpected changes. The **mtab** changes are certainly spurious, but the **passwd** changes might or might not be. Perhaps the installation script for **foobar** created a dedicated system account for it, or perhaps someone else edited the **passwd** file and forgot to commit their changes to the repository.

To resolve the question, you can run **git diff passwd** to see the actual changes in the **passwd** file. Let’s assume that in this case the **passwd** changes are unrelated to our recent activities. Therefore, we’ll probably want to check in these changes separately from the ones we just made:

```
$ sudo git commit passwd -m "Checking in existing passwd changes"
Created commit 6f7853c: Checking in existing passwd changes
 1 files changed, 1 insertions(+), 0 deletions(-)
```

We can make Git ignore the **mtab** file, now and forever; however, two steps are required. First, we’ll “delete” **mtab** from the current repository image:

```
$ sudo git rm --cached mtab
rm 'mtab'
```

The **--cached** option prevents Git from actually deleting the **mtab** file, so don’t leave it out! In essence, we’re stuffing a virtual file deletion operation into Git’s staging area. Git will behave as if we had deleted the file with **rm**.

The second step to eradicating **mtab** from Git’s universe is to add it to Git’s list of files to ignore in the future. That’s done by creating or editing a **.gitignore** file.

9. Even though this command makes no changes, it must still be run as root because it creates lock files in the **.git** directory.