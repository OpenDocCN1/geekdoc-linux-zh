9. Use the :wq command to save and exit the file. Make a backup, using the date (seconds) to create a unique file name.

![](bbox=[0.176, 0.098, 0.822, 0.403])

```
[student@workstation ~]$ cp editing_final_lab.txt editing_final_lab_$(date +%F).txt
```

10. Append a dash to the file. The dashed line should contain at least 12 dashes.

```
[student@workstation ~]$ echo "------------------------------------------------" >> editing_final_lab.txt
```

11. Append a directory listing of the Documents directory. List the directory listing on the terminal and edit the file with one command.

```
[student@workstation ~]$ ls Documents/ | tee -a editing_final_lab.txt lab_review.txt
```

```
[student@workstation ~]$ cat editing_final_lab.txt
-rw- 1 student 310 Jan 21 .bash_history
-rw- 1 student 18 Oct 12 .bash_logout
-rw- 1 student 141 Oct 12 .bash_profile
-rw- 1 student 312 Oct 12 .bashrc
drwx 0 student 201 Jan 14 .cache
drwx 10 student 203 Jan 14 .config
drwx 2 student 6 Jan 14 Documents
drwx 2 student 6 Jan 14 Downloads
-rw- 1 student 0 Jan 22 editing_final_lab.txt
-rw- 1 student 16 Jan 14 .sed_auth
-rw- 1 student 310 Jan 14 .ICEauthority
drwx 3 student 19 Jan 14 .local
drwx 2 student 6 Jan 14 Music
drwx 2 student 6 Jan 14 Pictures
```

12. Confirm that the directory listing is at the bottom of the file.