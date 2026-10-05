# Managing files from the Command Line

```
[student@server ~]$
```

18. Create a hard link to the ~/Documents/project_plans/season2_project_plan.odf file named ~/Documents/backups/season2_project_plan.odf.bak A hard link will protect against accidental deletion of the original file and will keep the backup file updated as changes are made to the original.

Notice that the link count is 2 for both season2_project_plan.odf.bak and season2_project_plan.odf files.

```
[student@server ~] mkdir ~/Documents/backups
[student@server ~] ln ~/Documents/project_plans/season2_project_plan.odf \
> ~/Documents/backups/season2_project_plan.bak
[student@server ~] ls -lR ~/Documents/
/home/student/:
total 0
drwxr-xr-x. 2 student student 43 Jan 31 18:59 backups
drwxr-xr-x. 4 student student 36 Jan 31 19:42 my_bestseller
drwxr-xr-x. 2 student student 70 Jan 31 19:20_project_plans

/home/student/backups:
total 4
-rw-rw--r--. 2 student 0 Jan 31 19:05 season2_project_plan.odf.bak

/home/student/my_bestseller:
total 0
drwxr-xr-x. 2 student student 118 Jan 31 19:39 chapters
drwxr-xr-x. 2 student student 62 Jan 31 19:38 editor

/home/student/my_bestseller/chapters:
total 0
-rw-rw--r--. 1 student 0 Jan 31 19:18 mystery_chapter3.odf
-rw-rw--r--. 1 student 0 Jan 31 19:18 mystery_chapter4.odf
-rw-rw--r--. 1 student 0 Jan 31 19:18 mystery_chapter5.odf
-rw-rw--r--. 1 student 0 Jan 31 19:18 mystery_chapter6.odf

/home/student/project_plans:
total 4
-rw-rw--r--. 1 student 0 Jan 31 19:20 season1_project_plan.odf
-rw-rw--r--. 2 student 0 Jan 31 19:05 season2_project_plan.odf
```

19. Exit from server.

```
[student@server ~] exit
logout
Connection to server closed.
[student@workstation ~]
```