```
```
root@ubuntu:~# mongodump
2022-09-22T22:36:54.838+0000      writing admin.system.version to dump/admin/system
    .version.bson
2022-09-22T22:36:54.839+0000      done dumping admin.system.version (2 documents)
2022-09-22T22:36:54.839+0000      writing school.students to dump/school/students.b
    son
2022-09-22T22:36:54.839+0000      done dumping school.students (2 documents)
root@ubuntu:~# tree dump/
dump/
├── admin
│   ├── system.version.bson
│   └── system.version.metadata.json
└── school
    ├── students.bson
    └── students.metadata.json

2 directories, 4 files
```
```

*Figure 11.43: Output example for command MongoDB and directory structure*

# Conclusion

Databases are important services for most of the applications. This chapter covered the use of relational databases and non-relational databases. Relational databases are popular for regular uses, such as Web applications or service applications. Non-relational databases are popular for applications and solutions that do not require having a strict model but instead require fast access to the data.

This chapter covered two of the most popular relational databases available on Linux systems: **MariaDB** (as a fork of **MySQL**) and **SQLite**. For NoSQL databases, the solution covered was the popular **MongoDB**.

# Key facts

+   - **MariaDB** is one of the most popular relational database management systems.
+   - **SQLite** is a database library. It is a perfect lightweight solution for applications.
+   - NoSQL gives freedom to developers, and its use in modern applications is popular.
+   - **MongoDB** is one of the most popular and easy NoSQL databases to use.

# Questions

+   1. What is the default main file for **MariaDB** (and **MySQL**)?