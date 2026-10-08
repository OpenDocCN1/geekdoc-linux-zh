+   4. Find the part of the configuration file that defines the port number and bind address. Remove the comments from those parameters.

Comments encapsulate the configuration parameters with these character strings: `<!--` and `-->`.

+   5. Remove the comments and the code should look like this:

```
<!-- You can use these two if you only want a single listener -->
<port>8000</port>
<bind-address>127.0.0.1</bind-address>
```

These parameters tell the Icecast2 server which port number and IP address to listen to. They also define the master server as the same machine.

+   6. Find the Master Server section of the configuration and remove the comments. The configuration should look like this:

```
<master-server>127.0.0.1</master-server>
<master-server-port>8001</master-server-port>
<master-update-interval>120</master-update-interval>
<master-password>hackme</master-password>
```

+   7. Find the <logdir> parameter and change it to

```
<logdir>/var/log/icecast</logdir>
```

This location is where all the information about the running Icecast2 server is kept (in logs). Information about Icecast2 problems is placed there too.

+   8. Find the <security> section. You should set the Icecast2 server to use the user and group identification number nobody:

```
<security>
  <chroot>0</chroot>
  <!--
    <changeowner>
      <user>nobody</user>
      <group>nobody</group>
    </changeowner>
  -->
</security>
```

Running the server as nobody reduces the security risk — breaking into your Icecast2 server doesn’t provide a hacker with superuser privileges.

+   9. Remove the comments from before the <changeowner> parameter and after the </changeowner> parameter: