# SETTING UP YOUR SYSTEM

This book presumes you are using the Linux operating system with either a KDE or Gnome desktop. Specific set-up instructions for common architectures are at http://www.ubiq.org/CProgrammingInLinux/

If you are using the KDE desktop you will have Konqueror or Dolphin as the File Manager and kate or kedit for an editor

In Gnome you would probably use Nautilus and gedit

You need to be familiar with the idea of doing some things as “super user” so that you have access permission to copy or edit certain files. This is normally done by prefacing the Linux command with “sudo” and providing the password, as in this example:

“sudo cp hello3 /srv/www/cgi-bin/hello3”

which copies the file “hello3” to the area where the Apache server locates common gateway interface or cgi programs.

In KDE “kdesu konqueror” would open a file manager as super user.

In Gnome “gnomesu nautilus” would open a file manager as super user.

You will need to have installed the following packages:

| package | Ubtunu | Open Suse |
| :--- | :--- | :--- |
| C development libraries | build-essential | Base Development (pattern) |
| Apache web server | apache2 | Web and LAMP Server (pattern) |
| Apache development libraries | apache2-prefork-dev | apache2-devel |
| MySQL server, client and development libraries | mysql-server libmysqlclient-dev | libmysqlclient-devel |
| GD and development libraries | libgd2-xpm libgd2-xpm-dev | gd gd-devel |