
These steps help you prepare your Fedora Core computer to start building the multimedia server:

- 1. Log in to your computer as any user.
- 2. Open Mozilla, go to www.icecast.org, and click the Download link at the top of the page.

Now you have to download the icecast2 and ices2 software from the Internet.

- 3. Click the icecast-2.0.2.tar.gz link.

A dialog box labeled Opening icecast-2.0.2.tar.gz opens.

- 4. Click the Save it to disk option and then click the OK button.

A dialog box labeled Enter name of file to save to... opens.

- 5. Click the Save button.

The file is downloaded to your computer.

- 6. Back in your browser, scroll down the page and click the libshout-2.0.tar.gz link.

The Enter name of file to save to... dialog opens.

- 7. Click the Save button and the libshout archive file is downloaded to your computer.

- 8. Once again, back in the www.icecast.org Web page, click the Ices link at the top, right of the page.

The Ices download page opens. Now it's time to download the ices2 source code.

- 9. Click the ices-2.0.0.tar.gz link.

A dialog box labeled Enter name of file to save to... opens.

- 10. Click the Save button.

The ices2 file is downloaded into your current directory.

Note that in this section, we break our unstated rule of installing only pre-compiled software from RPM packages. Although Icecast2 is available in RPM format, ices2 is not. We could use the Icecast2 package, but it requires a library (software that's shared between many programs) that's difficult to find. Therefore, compiling Icecast2 and Ices2 from scratch turns out to be easier. (It's also fun to know how we nerds spend our Saturday nights!)

Before installing Icecast2 and Ices2, we have to install the libshout libraries:

- 1. Open a terminal window by clicking the GNOME Menu and choosing System Tools:: Terminal.

These instructions assume that you're working from your home directory.

- 2. **Change to become the root user:**

```
su
```

Note that we don't use the su - command. Using the dash (-) tells the substitute user (su) command to adopt the new user's environment and change to the new user's home directory. That would include changing to the user home directory and complicate this process.

- 3. **Unpack the libshout archive and change to the new libshout directory.**

```
tar xzf libshout*
cd libshout-2.0
```

- 4. **Run the following command to set up the compilation process:**

```
./configure
```

- 5. **Compile and link the software by running the make command:**

```
make
```

- 6. **Install the software:**

```
make install
```

The libshout library is installed into /usr/local/lib. The following instructions show how to configure, compile and install Ices2 multimedia server.

- 1. **Go back up one level to your home directory:**

```
cd ..
```

- 2. **Unpack the Ices2 archive:**

```
tar xzf ices-2*
```

The asterisk matches any characters after the major version number — 2. We use it here just in case the Ices2 version number has changed.

- 3. **Change to the Ices2 directory that you created with the tar command in Step 2:**

```
cd ices-2*
```

- 4. **Run the following command to set up the compilation process:**

```
./configure
```

- 5. **Compile and link the software by running the make command:**

```
make
```

- 6. **Install the software:**

```
make install
```

The Ices2 software is installed in the /usr/local directories.

- 7. Copy the sample configuration file to its working location and move up one level:

```
cp conf/ices*.xml /usr/local/etc
cd ..
```

Next, use the following to configure, compile and install icecast2.

- 1. Unpack the icecast2 archive:

```
tar xzf icecast*
```

- 2. Change to the newly created icecast2 directory:

```
cd icecast*
```

- 3. Configure icecast2 for compilation:

```
./configure
```

- 4. Compile the source code:

```
make
```

- 5. Install the code:

```
make install
```

The icecast2 software is installed in the /usr/local directories.

- 6. Copy the sample configuration file to its working location:

```
cp conf/icecast2dist /usr/local/etc/icecast.conf
```

Your ices2 and icecast2 servers are now ready for prime time. The following section describes how to configure both systems. After they're configured, you can serve up multimedia streams.

## Configuring Icecast2

Ices2 gets its multimedia content from static files, such as music formatted in Ogg/Vorbis. Ices2 then feeds the audio streams to the icecast2 server. You can then connect to the icecast2 server with your client application to listen to the music. All these connections are made over IP networks.

Ices2 and icecast2 use the loopback (127.0.0.1) interface to communicate. (*The loopback interface is an internal network interface that doesn’t use any physical device.*) Using the loopback interface provides a simple method for testing your configuration.

> Icecast2 uses Port 8000 to communicate with its stream source and Port 8001 for administration.

You begin by configuring Icecast2:

- 1. Create the icecast user.

```
useradd -m -d /var/log/icecast icecast
```

This user will be run the icecast server, but will not function as a login account because we don't set a password.

- 2. Change to the /usr/local/etc directory.

- 3. Open the Icecast2 configuration file, like this:

```
gedit icecast.xml
```

Now, you have to make some minor modifications to the configuration file to set up your simple streaming server.

- 4. Find the part of the configuration file that defines the port number and bind address — 127.0.0.1. Remove the comments from those parameters.

Comments encapsulate the configuration parameters with these character strings: `<!--` and `-->`.

- 5. Remove the comments and the code should look like this:

```xml
<!-- You can use these two if you only want a single listener -->
<port>8000</port>
<bind-address>127.0.0.1</bind-address>
```

These parameters tell the Icecast2 server which port number and IP address to listen to. They also define the master server as the same machine.

- 6. Find the Master Server section of the configuration and remove the comments. The configuration should look like this:

```xml
<master-server>127.0.0.1</master-server>
<master-server-port>8001</master-server-port>
<master-update-interval>120</master-update-interval>
<master-password>hackme</master-password>
```

- 7. Find the `<logdir>` parameter and change it to this:

```xml
<logdir>/var/log/icecast/</logdir>
```

This location is where all the information about the running Icecast2 server is kept (in logs). Information about Icecast2 problems is placed there too.

- 8. Find the `<security>` section and change the user and group to icecast:

```
<security>
  <chroot>0</chroot>
  <!--
    <changeowner>
      <user>nobody</user>
      <group>nogroup</group>
    </changeowner>
  -->
</security>
```

Running the server as nobody reduces the security risk — breaking into your Icecast2 server doesn't provide a hacker with superuser privileges.

- 9. Remove the comments from before the `<changeowner>` parameter and after the `</changeowner>` parameter:

```
<security>
  <chroot>0</chroot>

  <changeowner>
    <user>icecast</user>
    <group>icecast</group>
  </changeowner>

</security>
```

Removing the comments allows the `<user>` and `<group>` directives to become active and force Icecast2 to run as user and group nobody. If you don't remove the comments, Icecast2 runs as the user and group of the process that starts it. Because you're logged in as root, Icecast2 runs as the root user.

![](img/41feae212f5c6612ff709354891f7b39_302_0.png)

Running any service as root can compromise your computer's security.

- 10. Save your changes by clicking the Save button.
- 11. Quit Gedit by selecting File → Quit.

You just started your multimedia server, but aren't transmitting anything. You have dead air now. Because you don't want to run afoul of the FCC, the next section describes how to configure and start the Ices2 server so you can feed content to the Icecast2 server.

## Configuring Ices2

Configuring Ices2 is similar to configuring Icecast2. Follow these steps to configure Ices2 and then feed an audio stream to Icecast2:
