# # Practice Questions

# ## Question 1

+   Which command is used to determine the default access mode for files when they are created?
+   
+   - a. `setfacl`
+   - b. `chmod`
+   - c. `umask`
+   - d. `getfacl`
+   - e. `ls`

Answer c is correct. The umask command determines the default access mode for files when they are created. The setfacl and chmod commands set access modes of existing files. Therefore, answers a and b are incorrect. The getfacl and ls commands display access modes of existing files. Therefore, answers d and e are incorrect.

# ## Question 2

+   Which of the following are true about the listing produced by executing the `ls -F` command? (Select all that apply.)
+   
+   - ☐ a. The names of directories are followed by a forward slash (`/`).
+   - ☐ b. The names of symbolic links are followed by an asterisk (`*`).
+   - ☐ c. The names of directories are followed by a plus sign (`+`).
+   - ☐ d. The names of executable files are followed by an asterisk (`*`).
+   - ☐ e. The names of symbolic links are followed by an ampersand (`@`).

Answers a, d, and e are correct. In the listing that results from the `ls -F` command, directory names are followed by a forward slash, executable filenames are followed by an asterisk, and symbolic link names are followed by an ampersand. Symbolic links are not followed by an asterisk. Therefore, answer b is incorrect. Directory names are not followed by a plus sign. Therefore, answer c is incorrect.