From your server of choice, download the latest version of MySQL (the one with the highest version number). At the time of this writing, this was 3.23.4.

# Note

There is, in fact, a binary rpm version of MySQL available at www.mysql.com. However, this is intended for Red Hat Linux and may not work with Caldera OpenLinux.

# Caution

MySQL 3.23.4 is a so-called “alpha” release. This is a release that has many of the features that will be included in the next stable release but can contain bugs and may, in some environments, be unstable. If stability is a great concern for you (and you are planning to store important data with MySQL), I recommend that you use the latest stable release. At this time of writing, this was 3.22.26a. However, it’s very possible that this has changed. A whole new stable distribution may have been released. Read about this on www.mysql.com.

# Installing the Files

When you have downloaded the source distribution, go to the directory containing the distribution file and unpack it:

```
# tar xvzf mysql-3.23.4-alpha.tar.gz
```

You will now see a lot of output from tar showing which files are included in the archive. When this is done, cd to your new mysql directory (in my case, this was /mysql-3.23.4-alpha).

In the mysql distribution directory, you need to run the `configure` script included there. When you run `configure`, all the “Makefiles” and other configuration files are edited automatically to suit your system. You will not be able to compile the source successfully by without running `configure` first. I would also add the option `--prefix=/usr/local/mysql` to `configure`. This will make MySQL install to /usr/local/mysql instead of /usr/local. I think this gives a better overview of the distribution, and I recommend that you do this, although it’s not required for the installation to work.

```
# ./configure --prefix=/usr/local/mysql
```