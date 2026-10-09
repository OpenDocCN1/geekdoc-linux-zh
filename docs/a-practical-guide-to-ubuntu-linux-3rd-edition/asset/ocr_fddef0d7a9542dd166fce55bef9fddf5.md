# ServerSignature  *Adds a line to server-generated pages.*

ServerSignature On | Off | Email

**On:** Turns the signature line on. The signature line contains the server version as specified by the ServerTokens directive (discussed on the preceding page) and the name specified by the <VirtualHost> container (page 918).

*Off:* Turns the signature line off.

*Email:* To the signature line, adds a mailto: link to the server email address. This option produces output that can attract spam. See ServerAdmin (page 912) for information on specifying an email address.

Contexts: server config, virtual host, directory, .htaccess
Specify in httpd.conf or sites-available/*
Default: Off
Ubuntu: On

# ## CONFIGURATION DIRECTIVES

# Group  *Sets the GID of the processes that run the servers.*

Group #groupid | groupname

where #groupid is a GID value, preceded by #, and groupname is the name of a group. The processes (servers) that Apache spawns are run as the group specified by this directive. See the User directive (page 929) for more information.

Context: server config
Specify in httpd.conf
Default: #1
Ubuntu: www-data

# Include  *Loads directives from files.*

Include filename | directory

where filename is the relative pathname of a file that contains directives. Apache prepends ServerRoot (page 926) to filename. The directives in filename are included in the file holding this directive at the location of the directive. Because filename can include wildcards, it can specify more than one file.

The directory is the relative pathname that specifies the root of a directory hierarchy that holds files containing directives. Apache prepends ServerRoot to directory. The directives in ordinary files in this hierarchy are included in the file holding this directive at the location of the directive. The directory can include wildcards.

Ubuntu Linux categorizes and splits Apache configuration information into files and directories related to virtual hosts, server configuration, ports, modules, and miscellaneous configuration options. These files are incorporated into the main apache2.conf file using Include directives; see page 906 for more information.