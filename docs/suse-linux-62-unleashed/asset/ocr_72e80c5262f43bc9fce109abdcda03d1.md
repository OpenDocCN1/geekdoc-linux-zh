# Networking and Internet Services
PART II

First, we will enter the /tmp directory, extract the xchat source tarball and enter the newly created source directory:

```
cd /tmp
tar xzf /path/to/file/xchat-1.2.0.tar.gz
cd xchat-1.2.0
```

Now, we need to run the configure script included in the directory. You will need to decide whether or not you want to enable GNOME support. If you are using GNOME, then you can just type ./configure. Otherwise, type ./configure -disable-gnomex, as shown here:

```
./configure --disable-gnome
```

After a host of configuration checks scroll by, it's time to create xchat by running make:

```
make
```

After compilation completes successfully, you'll want to install xchat:

```
make install
```

xchat will now be installed. As a non-root user, type xchat to start the program. You will be presented with a Server List window, which will allow you to enter your real name and select your preferred nicknames. In addition, this window provides a highly organized list of IRC servers worldwide, and allows you to organize your servers by group (see Figure 13.2). We will select OpenProjects.net, then choose the server of your choice that is listed underneath. Click Connect.

FIGURE 13.2
xchat Server List Window.

![](bbox=[0.283, 0.663, 0.741, 0.923])