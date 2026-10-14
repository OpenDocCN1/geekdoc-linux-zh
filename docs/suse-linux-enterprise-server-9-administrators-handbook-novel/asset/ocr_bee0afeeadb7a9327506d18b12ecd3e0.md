point would be the `dir` alias in Listing 5.2 that allows for DOS-type commands to appear to work in Linux.

To allow user-based customizations, `bash` also interprets scripts in the user's directory. At login, `bash` runs the first of the following files it finds in the user's directory: `.bash_profile`, `.bash_login`, or `.profile`. These local scripts can be used to set or override variables to better suit the end user's requirements. A typical snippet of a `.bash_profile` would look like Listing 5.3. In this snippet, you can see that two environment variables, `BACKUP_DIR` and `WEB`, are created, as well as an alias. The alias `stat`, short for status, yields information on the current logged-on process, disk quota usage, as well as a summary of disk space in the user's home directory. When the user is logged in, the variables have the username of the current session in the proper locations, as shown in Listing 5.4. It is important to note that an alias is not evaluated at login; it is evaluated when invoked.

# **LISTING 5.3**  
Content of a typical `.bash_profile`

```
```bash
BACKUP_DIR=/backup/$USER ; export BACKUP_DIR
WEB="/home/$USER/public_html" ; export WEB
alias stat='finger $USER ; quota $USER ; du --si -s $HOME'
```
```

# **LISTING 5.4**  
Verification of Environment Variables After Login

```
```bash
eric@Athena:~> env | grep -e BACKUP
BACKUP_DIR=/backup/eric
eric@Athena:~> env | grep -e WEB
WEB=/home/eric/public_html
eric@Athena:~> alias -p | grep -e st=
alias st='finger $USER ; quota $USER ; du --si -s $HOME'
eric@Athena:~>
```
```

When the `$USER` symbol is placed in the definitions in Listings 5.3 and 5.4, the `.bash_profile` script is more portable from machine to machine and user to user. A user with a privileged account on one machine, such as WEBMASTER, should have a regular account, such as eric on other servers. By using standard variables provided by bash, the login script becomes user-independent.

Upon logout, the bash shell calls one final script: `.bash_logout`. If this file exists at logout time, it will be executed. Users can set up routines to back up files or force a cleanup of temporary files. Here is the content of a sample `.bash_logout`: