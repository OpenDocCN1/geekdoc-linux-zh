where `<Server-Hostname>` is the documentation Web server's hostname or IP address.

+   You can run DocSearch and the man pages from a mounted CD-ROM, but this method is not recommended because response time can be unacceptable, and, the CD-ROM must always be mounted for the documentation service to work.

+   The entire documentation search services library should be installed on a fixed disk local to the documentation server for optimal performance.

+   To install DocSearch on AIX 4.3.3, you need to define an **innadm** user and group if they do not already exist and ensure that the language environment variable is set to the correct value.

+   By default, the DocSearch Library Search Services are installed as part of BOS on AIX 5L. However, if you did a *migration upgrade* from a previous AIX version or release, you could have a few problems getting the documentation search services working again and may want to uninstall and reinstall the DocSearch system.

+   In the main DocSearch browser window, to perform a search, enter the topic of interest in the Search For field and press the ENTER key. Your search can be a simple word or phrase match, or you can create complex logical search using the AND, OR, and NOT logical search operators.

+   You could have a problem with DocSearch domain name registration. If so, edit the `/etc/hosts` file and add a period (.) right behind the short hostname.

+   To display reference documentation about AIX commands, files, library subroutines, and system calls, use the **man** command.