# Advanced Topics

This section walks you through getting a PostgreSQL server installed and running, then setting up a user account and database to work with in your shell scripts.

# Installing PostgreSQL

Just like MySQL, you can install the PostgreSQL database server package either by using your system's automated software installation system, or manually by downloading it from the PostgreSQL Web site.

To use your Linux distribution's automated software installation, follow the same procedures outlined in the "Installing MySQL" section earlier. If you must manually download the PostgreSQL server software, unfortunately you'll have to do a little more work than MySQL.

The only binary distribution for PostgreSQL software uses the Red Hat RPM management system. If your Linux system uses that management system (or the Debian distribution, which uses a utility to convert an RPM package into its own format), you can download the binary package and install it.

If not, you'll need to download the source code package for PostgreSQL, and manually compile it on your Linux system. This can be an interesting project.

> Compiling a source code package requires that you have the C software development package loaded onto your Linux system. These days is a common thing for servers, but it may not be loaded if you're using a desktop Linux distribution. Please consult your individual Linux distribution documentation regarding compiling source software, and what software packages are required for compiling C source code projects.

Here are the steps to obtain the PostgreSQL source code and install it in your system:

+   1. Open a browser window to the URL: www.postgresql.org.
2. Select the Source link for the latest PostgreSQL version at the top-right corner of the Web page.
3. Select the appropriate download file format (either using bzip2 or gzip) to download.
4. Select the download mirror site and method to begin the download.

After downloading the code, place it in a working directory on your Linux system (such as your $HOME directory), and extract the package files using the tar command:

```
tar -zxvf postgresql-8.2.6.gz
```

The tar command creates the directory postgresql-8.2.6 (or whatever version you've downloaded) in your working directory and extracts the source code files. You're now ready to start building.

Here are the steps you'll need to create the PostgreSQL server and client executable files:

+   1. Change to the new directory that contains the PostgreSQL source code.
   $ cd postgresql-8.2.6