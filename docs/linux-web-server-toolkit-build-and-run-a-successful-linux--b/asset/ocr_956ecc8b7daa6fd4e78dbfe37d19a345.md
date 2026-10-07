# Chapter 11: Configuring the Apache Web Server

defined by this directive, the Web server will attempt to run the file as a program instead of simply returning the contents of the file. The following is the default value of the directive:

ScriptAlias /cgi-bin/ /home/httpd/cgi-bin/

The default says that any document requested using a filename in the /cgi-bin directory will actually be located in /home/httpd/cgi-bin and should be executed instead of returned for display.

You can list several aliases anywhere on your server. Remember the items noted in Chapter 10 about using scripts and use the ScriptAlias directive with caution, noting the permissions of the directories you place in ScriptAlias directories and checking the files in that directory to see that they can be executed and provide valid results.

When you use the ScriptAlias directive, note that the “fake name” of the directory is listed first, followed by the real directory on the Web server where the scripts are located. This is the opposite of the ln command in UNIX used to create a symbolic link (file alias).

The remainder of the directives in the srm.conf default file are commented out. These lines are examples of more advanced features that are described later in this chapter.

# Changing the Default Settings

The settings in the default srm.conf file should be sufficient for a standard Web server. Because the settings in srm.conf are informational in nature, they pose no security threat. However, they operate with other settings that do require vigilance, as you'll read in the next section on access.conf.

You might review the Indexno directive if you want to have indexing (automatic generation of directory listings) available if you are concerned that some common files in your directories are not shown in lists.

The AddEncoding directives can be altered to match the capabilities that you want to offer. Those listed in the default file are part of OpenLinux; you might find a Linux version of PKZip that would add a useful feature for non-UNIX browsers.

It is important that the directories under the ScriptAlias directive be listed in the access.conf file with restrictive rights.

The many other sample settings in the default srm.conf file are examples of advanced features described later in this chapter.

The srm.conf file defines what resources on your Web server are used to send information to browsers. The next section describes the third Apache configuration file, access.conf, which is used to manage the security of your Web server.