You begin by configuring Icecast2:

+   1. Create the icecast user.
+      
+      ```
+      useradd -m -d /var/log/icecast icecast
+      ```
+      This user will be run the icecast server, but will not function as a login account because we don't set a password.

+   2. Change to the /usr/local/etc directory.

+   3. Open the Icecast2 configuration file, like this:
+      
+      ```
+      gedit icecast.xml
+      ```
+      
+      Now, you have to make some minor modifications to the configuration file to set up your simple streaming server.

+   4. Find the part of the configuration file that defines the port number and bind address — 127.0.0.1. Remove the comments from those parameters.
+      
+      Comments encapsulate the configuration parameters with these character strings: <! -- and -->.

+   5. Remove the comments and the code should look like this:
+      
+      ```xml
+      <!-- You can use these two if you only want a single listener -->
+      <port>8000</port>
+      <bind-address>127.0.0.1</bind-address>
+      ```
+      
+      These parameters tell the Icecast2 server which port number and IP address to listen to. They also define the master server as the same machine.

+   6. Find the Master Server section of the configuration and remove the comments. The configuration should look like this:
+      
+      ```xml
+      <master-server>127.0.0.1</master-server>
+      <master-server-port>8001</master-server-port>
+      <master-update-interval>120</master-update-interval>
+      <master-password>hackme</master-password>
+      ```

+   7. Find the <logdir> parameter and change it to this:
+      
+      ```xml
+      <logdir>/var/log/icecast/</logdir>
+      ```
+      
+      This location is where all the information about the running Icecast2 server is kept (in logs). Information about Icecast2 problems is placed there too.

+   8. Find the <security> section and change the user and group to icecast: