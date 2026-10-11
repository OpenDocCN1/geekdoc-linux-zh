794   Appendix A  Obtaining and Installing Software

```
```text
[mysql14]
basedir=C:/mysql
dataDir=C:/mysql1/data
```
```

If you select a different installation directory, you’ll need to change the pathnames in the option file.

MySQL distributions for Windows include several servers, each of which is built with different options:

+   - Prior to MySQL 5.1.21, *mysql1*-nt and *mysql14* are separate servers with and without support for named pipes, respectively.
+   - As of MySQL 5.1.21, *mysql14* includes support for named pipes and there is no separate *mysql1*-nt server.
+   - *mysql1*-debug in all versions has support for named pipes, debugging, and automatic memory allocation checking.

In general, unless you need the debugging support provided by the *mysql1*-debug server, you are better off choosing another server. *mysql1*-debug uses much more memory and runs more slowly than the other Windows servers.

For servers that support connections using named pipes, this connection type is disabled by default. All servers support shared-memory connections, but these too are disabled by default. To enable these capabilities, you must add the appropriate lines to the [mysql14] group in your option file:

```
```text
[mysql14]
enable-named-pipe
shared-memory
```
```

On Windows, any MySQL server can be installed to run as a service that starts automatically whenever Windows starts. For example, to install the *mysql14* server as a Windows service, use this command:

```
```bash
C:\> C:/mysql1/bin/mysql1 --install
```
```

The install command uses the full pathname to the server. If the server is installed in a different location, modify the pathname accordingly.

If you use --install-manual rather than --install, the server is installed as a Windows service, but does not run automatically when Windows starts. You must use the Windows Services Manager or the net start command.

If you install a MySQL server as a Windows service, you can specify other options by putting them in the [mysql14] group of an option file.

For a server that is installed as a service, you can start it manually using the Windows Services Manager. You should be able to find this as a Services item in the Windows Control Panel or in the Administrative Tools item in the Control Panel. The service also can be started using the following command:

```
```bash
C:\> net start MySQL
```
```