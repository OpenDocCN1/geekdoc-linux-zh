Next, edit the /var/yp/secure nets file (or create a new file if it does not exist) to specify the IP addresses of client computers that can access the NIS maps. For example, to allow connections from the localhost and hosts in the 192.168.0.0 network, use the following as the content of the /var/yp/secure nets file:

```
# Always allow access for localhost
host 127.0.0.1
# allow connections from any host
# on the 192.168.0.0 network
255.255.255.0 192.168.0.0
```

The last line allows only those computers in the range 192.168.0.1 through 192.168.0.254 to access the NIS maps.

Next, you should generate the NIS map database by running the /usr/lib/yp/ypinit program with the -m option. Here is a sample session with that program:

```
/usr/lib/yp/ypinit -m
```

The program asks you for names of hosts that will run NIS servers. It automatically selects your host as an NIS server and prompts for the names of any other NIS servers. You can add the server names one at a time and press Ctrl-D when you're done. Then you have to verify that the list of NIS servers is correct (type y). After that, the program generates the NIS maps as specified by the all: line in the Makefile. The map files are stored in a subdirectory of /var/yp that has the same name as the NIS domain name you have previously set for your system. For example, for the NIS domain admin, the map files are in the /var/yp/admin directory.

# Master NIS server configuration

To configure the NIS server daemon, ypserv, you have to prepare the configuration file /etc/ypserv.conf. You can learn about the syntax of this file by typing the command man ypserv.conf.

You can add lines in /etc/ypserv.conf that specify access rules — which hosts can access which maps. The format of the access rules is as follows:

```
Host : Map : Security : mangle [: field_to_mangle]
```

The field_to_mangle is optional; it indicates which field in the map file should be mangled (the default is the second field because the password is in the second field of most files, such as /etc/passwd). To mangle a field is to replace it with an x if the request comes from an unprivileged host. The rest of the fields have the following meanings: