+   2. Change the file mode to -rwxr--r-- using the symbolic format. 
+   3. Repeat the operation in Question 2 using the numeric (octal) format. 
+   4. Assume that the jobs directory contains the joblog file. Using 
+   ls -lR should verify it:

```
$ ls -lR<Enter>
total 8
drwxr-xr-x5 perez knights2 4096 Jun 17 08:09 jobs
./jobs:
total 8
-rw-rw-r--1 perez knights2 100 Jun 18 13:22 joblog
```

Can Nicholas, who is a member of the knights2 group, modify the 
joblog file?

+   5. This question is based on the following listing. Assume that the jobs 
+   directory contains the work directory, which in turn contains the 
+   joblog file:

```
$ ls -lR<Enter>
total 8
drwxr-xr-x5 perez knights2 4096 Jun 17 08:09 jobs
./jobs:
total 8
drwxrwxr-x2 perez knights2 4096 Jul 21 09:41 work
./jobs/work:
total 8
-rw-rw-r--1 perez knights2 100 Jun 18 13:22 joblog
```

Can Nicholas, who is a member of the knights2 group, modify the 
file joblog?

+   6. This question is based on the following listing. Assume that the jobs 
+   directory contains the work directory (note that the permissions on 
+   work have been changed), which in turn contains the joblog file:

```
$ ls -lR<Enter>
total 8
drwxr-xr-x 5 perez knights2 40961 Jun 17 08:09 jobs
./jobs:
total 8
```