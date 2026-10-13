example, the user has a clear and an echo command in the .bash_logout file. When the user logs out, the clear command clears the screen, and then the echo command displays the message "Good-bye for now."

.bash_logout

```
# ~/.bash_logout
clear
echo "Good-bye for now"
```

# Initialization and Configuration Files

Each type of shell has its own set of initialization and configuration files. The Bash shell configuration files were discussed previously. The TCSH shell uses .login, .tcshrc, .logout files in place of .bash_profile, .bashrc, and .bash_logout. The Z shell has several initialization files: .zshenv, .zlogin, .zprofile, .zshrc, and .zlogout. See Table 9-2 for a listing. Check the Man pages for each shell to see how they are usually configured. When you install a shell, default versions of these files are automatically placed in the users' home directories. Except for the TCSH shell, all shells use much the same syntax for variable definitions and assigning values (TCSH uses a slightly different syntax, described in its Man pages).

Table 9-2: Shell Configuration Files

| File | Function |
|------|----------|
| **BASH Shell** | |
| .bash_profile | Login initialization file |
| .bashrc | BASH shell configuration file |
| .bash_logout | Logout name |
| .bash_history | History file |
| /etc/profile | System login initialization file |
| /etc/bashrc | System BASH shell configuration file |
| /etc/profile.d | Directory for specialized BASH shell configuration files |
| **TCSH Shell** | |
| .login | Login initialization file |
| .tcshrc | TCSH shell configuration file |
| .logout | Logout file |
| **Z Shell** | |
| .zshenv | Shell login file (first read) |
| .zprofile | Login initialization file |
| .zlogin | Shell login file |
| .zshrc | Z shell configuration file |
| .zlogout | Logout file |
| **PDKSH Shell** | |
| .profile | Login initialization file |