user.email data is stored in the global Git configuration file. Notice that you can view this information using the --get option and passing it the data's name as an argument.

> **NOTE**
> 
> **Global Git configuration information means that this data applies to all Git projects on this system. Local Git configuration information is applied only to a particular Git project stored within a working directory on the system.**

Git global configuration information is stored in the `.gitconfig` file within your home directory and the local repository, which is the working-directory/.git/config configuration file. Be aware that some systems have a system-level configuration file, which is /etc/gitconfig.

To view all the various configurations stored in these files, use the git config --list command:

```
$ git config --list
user.name=Christine Bresnahan
user.email=cbresn1723@gmail.com
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true
$
$ ls /home/christine/.gitconfig
/home/christine/.gitconfig
$
$ cat /home/christine/.gitconfig
[user]
    name = Christine Bresnahan
    email = cbresn1723@gmail.com

$
$ ls /home/christine/MwGuard/.git/config
/home/christine/MwGuard/.git/config
$
$ cat /home/christine/MwGuard/.git/config
```