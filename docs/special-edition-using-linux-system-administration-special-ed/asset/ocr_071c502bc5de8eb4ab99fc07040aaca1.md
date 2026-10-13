The difficulty lies in the fact that slave servers, once configured, expect to receive map updates from a specific master server and will reject maps pushed to them from other systems. This serves as a form of security and prevents unauthorized systems and users from setting up alternate master servers for a domain and attempting to push invalid map data to all the slaves.

To get around this problem, several steps are involved:

+   1. Creating the new master server as a slave server
+   2. Adding the new master server to the ypservers database
+   3. Copying the /etc configuration files from the old master to the new master
+   4. Copying the NIS makefile in /var/yp from the old master to the new master
+   5. Deleting the time stamp files from /var/yp on the new master
+   6. Running make with the NOPUSH=1 option
+   7. Transferring the new NIS maps from the new master server to the old master server
+   8. Pushing the new maps from the old master server to all slave servers
+   9. Retiring the old master server

# CREATING THE NEW MASTER SERVER AS A SLAVE SERVER

Follow the instructions in the section “Adding an NIS Slave Server” earlier in this chapter to set up your new master server machine as a slave in the NIS domain. In summary, the relevant steps are as follows:

+   1. Set the NIS domain name.
+   2. Run ypinit -s masterhostname.

# ADDING THE NEW MASTER SERVER TO THE ypservers DATABASE

The ypservers database is the NIS map that contains the hostnames of all NIS servers in the NIS domain. The new master server’s name must be added to the ypservers database. This is done by performing the following steps on the old NIS master server:

+   1. Take a snapshot of the database in a text file.
+   2. Edit the text file.
+   3. Regenerate the ypservers database from the file.
+   4. Push the new database to all slaves.

# TAKE A SNAPSHOT OF THE ypservers DATABASE

You can take a snapshot of any NIS database and save it to a file using the ypcat command. The ypcat command is discussed in detail later in this chapter.

The following command will dump a copy of the ypservers NIS map to the file /etc/ypservers:

```
```sh
# /usr/lib/yp/makedbm -u ypservers > /etc/ypservers
```
```