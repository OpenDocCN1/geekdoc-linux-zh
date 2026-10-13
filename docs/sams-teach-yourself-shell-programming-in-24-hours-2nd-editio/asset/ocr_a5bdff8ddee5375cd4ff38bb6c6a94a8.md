After these steps have been performed, a prompt is displayed. The default prompt for bash is bash$ (the string bash$ followed by a space).

# Z Shell

Z shell (zsh) initialization is quite long and does not resemble the initialization process of the other shells. It has 16 steps and involves the init files /etc/zshenv, .zshenv, /etc/zprofile, .zprofile, /etc/zlogin, and .zlogin:

+   1. zsh checks to see whether the file /etc/zshenv exists.
+   2. If it exists, zsh reads it; otherwise, zsh skips it.
+   3. zsh checks to see whether the file .zshenv exists in your home directory.
+   4. If it exists, zsh reads it; otherwise, zsh skips it.
+   5. zsh checks to see whether the file /etc/zprofile exists.
+   6. If it exists, zsh reads it; otherwise, zsh skips it.
+   7. zsh checks to see whether the file .zprofile exists in your home directory.
+   8. If it exists, zsh reads it; otherwise, zsh skips it.
+   9. zsh checks to see whether the file /etc/zshrc exists.
+   10. If it exists, zsh reads it; otherwise, zsh skips it.
+   11. zsh checks to see whether the file .zshrc exists in your home directory.
+   12. If it exists, zsh reads it; otherwise, zsh skips it.
+   13. zsh checks to see whether the file /etc/zlogin exists.
+   14. If it exists, zsh reads it; otherwise, zsh skips it.
+   15. zsh checks to see whether the file .zlogin exists in your home directory.
+   16. If it exists, zsh reads it; otherwise, zsh skips it.

After these steps have been performed, a prompt is displayed. The default prompt for zsh is host%. Here host is the hostname of your system. For example, on a system named nars, the default zsh prompt would be nars%.

# Initialization File Contents

Usually a shell's init files are quite short. The purpose of these files is to provide a complete working environment with as little overhead as possible. In this section, we will look at the basic settings required for Bourne shell. If you are using a different shell, you can put these settings into an init file used by that shell.