# Linux Hack

Ajay Kumar Tiwari

many files are open in the system at any given point of view as shown below.

```
# lsof | wc -l
```

3093

# View open files by a specific user

Use lsof –u option to display all the files opened by a specific user.

```
# lsof –u ramesh
```

```
vi7190 ramesh
475196 /bin/vi
txt
REG
8,1
474608
sshd7163 ramesh3u IPv615088263
TCP dev-db:ssh->abc-12-12-12-12.socal.res.rr.com:2631
(ESTABLISHED)
```

A system administrator can use this command to get some idea on what users are executing on the system.

# List Users of a particular file

If you like to view all the users who are using a particular file, use lsof as shown below. In this example, it displays all users who are currently using vi.

```
# lsof /bin/vi
```

```
COMMAND PID
vi7258
vi7300
USERFD
roottxt
ramesh txt
TYPE DEVICESIZENODE NAME
REG8,1 474608 475196 /bin/vi
REG8,1 474608 475196 /bin/vi
```