To check whether PostgreSQL is installed on your system, type **rpm -qa postgresql**$^1$. You see a list of at least three RPMs — *postgresql*, *postgresql-libs*, and *postgresql-server*. If a message informs you that the packages are not installed, you can install them from this book’s companion DVD using these steps:

+   **1. Log in as root and insert the DVD into the DVD drive.**
+   
+   If you are using GNOME or KDE, the DVD mounts automatically. If not, type the following command in a terminal window to mount the DVD:
+   
+   ```
+   mount /mnt/cdrom
+   ```
+   
+   If you have a primary CD-ROM drive and you added a second DVD/CD drive, type `mount /mnt/cdrom1` to mount the DVD.

+   **2. Type the following commands to install PostgreSQL:**
+   
+   ```
+   cd /mnt/cdrom/Fedora/RPMS
+   rpm -ivh postgresql*
+   ```
+   
+   The packages you need to use PostgreSQL install on your system.

To use PostgreSQL, you have to first log in as **root** and start the database server with the following command:

```
service postgresql start
```

The PostgreSQL server process starts, called *postmaster*. The server is a daemon (a background process that runs continuously) that accepts database queries from client processes and performs database tasks (such as adding tables) on behalf of clients.

If you want the PostgreSQL database server to start whenever your system starts, type the following command to turn it on:

```
chkconfig postgresql on
```

Now you have to design a database, create that database in PostgreSQL, and load it with the data. To illustrate how to create and load a database, I set up a simple book catalog database.

# ## Adding a database user

PostgreSQL has its own concept of users, separate from the Linux user accounts. To enable a user to access PostgreSQL databases on your system, you have to add that username as a PostgreSQL user.