# # NIS Components

NIS consists of four major components.

| Component | Description |
| :--- | :--- |
| Maps | NIS stores information such as user name, pass-word, and group name in database files; referred to as NIS maps. Each map consists of a pair of files. A map is made up of key-pair values and is stored in the database management library format. NIS maps can be created by running make in the /var/yp directory. |
| NIS Domain | An NIS domain is a group of hosts that share the same set of maps. The hosts within a domain share password, host, and group file information. Maps are stored in a subdirectory having the same name as the domain in the /var/yp directory. By default, the NIS domain name is specified in the /etc/ sysconfig/network file. Each domain consists of a single master NIS server. A client can belong to only one domain. |
| NIS Master Server | NIS stores the database that contains network infor-mation in the master server. The master server also contains the source files for various maps. The ypserv process should be run on the server to manage the NIS server. The configuration settings of the master server are specified in the ypserv.conf file that is stored in the /etc NIS directory. |
| NIS Slave Server | An NIS slave server is a secondary server that bal-ances the load on the master server. The slave server contains a copy of the database and source files. Any update made on the maps or database will be updated to the slave server by the master server using the yppush command. When the mas-ter server is down, then the slave server will act as a master server and resolve the queries sent by the client. The information about the slave server is specified in the /var/yp/ypservers file. |

# ## NIS Maps

There are many standard maps supported by NIS.

| File | Map | Description |
| :--- | :--- | :--- |
| /etc/hosts | hosts.byname, hosts.byaddr | Maps an IP address to the cor-responding hostname. |
| /etc/networks | networks.byname, networks.byaddr | Maps an IP network address to the network name. |