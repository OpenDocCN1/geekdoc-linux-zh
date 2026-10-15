a subdirectory of the NIS directory named for the NIS domain. The exact name and number of the map files depends on the hashing library being used. There is one map (file) for each key by which a file can be searched. For example, in the domain cssuns, the DB files for the /etc/passwd maps might be
/var/yp/cssuns/passwd.byname
/var/yp/cssuns/passwd.byuid

The makedbm command generates NIS maps from flat files. However, you need not invoke this command directly; a Makefile in /var/yp generates all the common NIS maps. After you modify a system file, cd to /var/yp and run make. The make command checks the modification time of each file against the modification times of the maps derived from it and runs makedbm for each map that needs to be rebuilt.

On HP-UX systems, a command called ypmake is used instead of make.

The ypxfr command copies maps from the master server to the slave servers. ypxfr is a pull command; it must be run on each slave server to make that server import the map. Slaves usually execute ypxfr every so often just to verify that they have the most recent maps; you can use cron to control how often this is done.

The default implementation of map copying is somewhat inefficient. On most systems, a daemon called ypxfrd (or rpc.ypxfrd) can be run on the master server to speed responses to ypxfr requests. ypxfrd sidesteps the normal NIS protocol and simply hands out copies of the map files. Unfortunately, map files are stored with different database formats and byte ordering on different systems, so the use of ypxfrd introduces some potential incompatibilities.

yppush is a "push" command that's used on the master server. It actually does not transfer any data but rather instructs each slave to execute a ypxfr. The yppush command is used by the Makefile in the NIS directory to ensure that newly updated maps are propagated to slaves.

The special map called ypservers does not correspond to any flat file. This map contains a list of all the servers of the domain. It's automatically constructed when the domain is set up with ypinit. Its contents are examined when the master server needs to distribute maps to slaves.