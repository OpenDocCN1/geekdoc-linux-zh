
## 12.2 Arranging for MySQL Server Startup and Shutdown

automatically during the system startup procedure. Methods for doing this include the following:

- **Invoke `mysqld` directly.** This is probably the least common method. I won't discuss it further, except to say that the following command is useful for finding out what startup options the server supports:
  ```
  % mysqld --verbose --help
  ```

- **Invoke the `mysqld_safe` script.** `mysqld_safe` invokes the server for you and then monitors it and restarts it if it terminates abnormally. `mysqld_safe` commonly is used on BSD-style versions of Unix, and it also is invoked by `mysql.server` on non-BSD systems and on Mac OS X.

  `mysqld_safe` redirects error messages and other diagnostic output from the server to `syslog` or to a file in the data directory to produce an error log. If you send error output to a file, `mysqld_safe` sets the ownership of the file so that it is owned by the login account named by the `--user` option. This can lead to trouble if you use different `--user` values at different times. The symptom is that `mysqld_safe`'s attempt to write to the error log file will fail with a “permission denied” error. This can be especially problematic because if you examine the error log to see what the difficulty is, it will contain no useful information related to the cause! If this problem occurs, remove the error log file and invoke `mysqld_safe` again.

- **Invoke the `mysql.server` script.** `mysql.server` starts the server by executing `mysqld_safe`. This script can be invoked with an argument of `start` or `stop` to indicate whether you want the server to start or stop. It serves as a wrapper around `mysqld_safe` and commonly is used on systems that employ the System V method of arranging startup and shutdown scripts into several directories. Each directory corresponds to a particular run level and contains scripts to be invoked when the machine enters or exits that run level.

- **To coordinate several servers, use the `mysqld_multi` script.** This script reads an option file in which you list startup parameters for multiple servers. It enables you to start or stop each one, or check whether it is running. This startup script is more complicated than the others, so I'll defer discussion to Section 12.10, “Running Multiple Servers.”

The `mysqld_safe` and `mysqld_multi` scripts are installed in the `bin` directory under the MySQL installation directory and can be found in the `scripts` directory of MySQL source distributions. The `mysql.server` script is installed under the `share/mysql` directory under the MySQL installation directory or can be found in the `support-files` directory of MySQL source distributions. If you want to use `mysql.server`, you might need to copy it to the proper run-level directory and make it executable. (Some installation methods install `mysql.server` for you. Linux RPM and Mac OS X DMG packages do so, for example.) If you use a MySQL RPM obtained from another vendor, a similar startup script might be installed under a different name, such as `mysql`.

The type of system you have determines the arrangements that you’ll need to make to have a startup script execute at system boot time. Read through the following examples and use or adapt the instructions that most closely match the startup procedures for your system.

For BSD-style systems, it’s common to have a few files in the `/etc` directory that initiate services at boot time. These files often have names that begin with *rc*, and it’s likely that there will be a file named `rc.local` (or something similar) intended specifically for starting locally installed services. On an *rc*-based system, you might add lines such as the following to `rc.local` to start the server:

```
if [ ! -x /usr/local/bin/mysqld_safe ]; then
fi
/usr/local/bin/mysqld_safe &
```

Modify the lines appropriately if the pathname to `mysqld_safe` is different on your system.

For System V-style systems, you can install `mysql.server`. Copy it to the appropriate run-level directory under `/etc`. This may have been done for you already if you run Linux and installed MySQL from an RPM package. Otherwise, install the script in the main startup script directory with the name you want to use, make sure the script is executable, and place links to it in the appropriate run-level directory.

> **Note**
>
> Normally, you install `mysql.server` into the run-level directory under the name `mysql`, but I’ll generally continue to discuss it as `mysql.server` to make it clear what I’m referring to.

The layout for run-level directories varies from system to system, so you’ll need to check to see how your system organizes them. For example, under Solaris, the general multi-user run level is 2. The main script directory is `/etc/init.d`, and the run-level directory is `/etc/rc2.d`. So the commands would look like this:

```
# cp mysql.server /etc/init.d/mysql
# cd /etc/init.d
# chmod +x mysql
# cd /etc/rc2.d
# ln -s ../init.d/mysql S99mysql
```

At system startup time, the boot procedure automatically invokes the `S99mysql` script with an argument of `start`.

Many Linux variants have a similar set of directories, but organized under `/etc/init.d` and `/etc/rc.d`. Such Linux systems typically have a `chkconfig` command that is intended for startup script management. You can use it to help you install the `mysql.server` script instead of manually running commands like those just shown. The following instructions show how to install `mysql.server` into the startup directories using a name of `mysql`:

1. Copy the `mysql.server` script from wherever it's located into the `init.d` directory and make it executable:
   ```
   # cp mysql.server /etc/init.d/mysql
   # chmod +x /etc/init.d/mysql
   ```
2. Register the script and enable it:
   ```
   # chkconfig --add mysql
   # chkconfig mysql on
   ```
3. To verify that the script has been properly enabled, run `chkconfig` with the `--list` option:
   ```
   # chkconfig --list mysql
   mysql    0:off    1:off    2:on    3:on    4:on    5:on    6:off
   ```

   That output indicates that the script will execute automatically for run levels 3, 4, and 5.
   If you don't have `chkconfig`, you can use a procedure similar to that used for Solaris, although the pathnames are slightly different. To enable the script for run level 3, use these commands:
   ```
   # cp mysql.server /etc/init.d/mysql
   # cd /etc/init.d
   # chmod +x mysql
   # cd /etc/rc.d/rc3.d
   # ln -s /etc/init.d/mysql S99mysql
   ```

Under Mac OS X, the startup procedure is different yet. The `/Library/StartupItems` and `/System/Library/StartupItems` directories contain subdirectories for the services that are initiated at system boot time. The DMG package provided for Mac OS X at the MySQL Web site contains an installer that places a startup item for the MySQL server into one of these directories.

### 12.2.2 Running the MySQL Server On Windows

On Windows, you can start the MySQL server manually from the command line. It's also possible to install the server as a Windows service. You can set the service to run automatically when Windows starts and control it from the command line or by using the Windows Services Manager.

MySQL distributions for Windows include several servers, each of which is built with different options. You can find a summary of the different servers in Appendix A. For this discussion, I'll use the name `mysqld` for examples, but your distribution might contain servers with different names such as `mysqld-nt` or `mysqld-debug`.

Windows servers provide two types of connections that Unix servers do not:

- Connections via named pipes, if the server is started with the `--enable-named-pipe` option.
- Connections via shared memory, if the server is started with the `--shared-memory` option.

Prior to MySQL 5.1.21, only the servers named `mysqld-nt` and `mysqld-debug` support named pipes. (The “nt” derives from the fact that named pipes are a feature first available in Windows NT, the predecessor to Windows 2000. `mysqld-debug` is like `mysqld-nt` with the addition of debugging support.) As of 5.1.21, all Windows servers are built with named-pipe support, and there are no longer any servers with -nt in the name.

#### 12.2.2.1 Running the Server Manually on Windows

To start a server manually, invoke it from the command line in a console window:

```
C:\> mysqld
```

If you want error messages to go to the console window rather than to the error log (the `host_name.err` file in the data directory), use the `--console` option:

```
C:\> mysqld --console
```

When you run a MySQL server from the command line, you will not necessarily see another command prompt until the server exits. That's okay. It just means that you need to open another console window to use for running client programs.

If you add the `--shared-memory` option to the startup command, the server enables local clients to connect using shared memory. Similarly, if your server was built with named-pipe support, start it with the `--enable-named-pipe` option to enable local clients to connect via named pipes.

To stop the server, use `mysqladmin`:

```
C:\> mysqladmin -p -u root shutdown
```

#### 12.2.2.2 Running the Server as a Windows Service

On Windows, any MySQL server can be installed as a Windows service using this command:

```
C:\> C:\mysql\bin\mysqld --install
```

The command uses the full pathname to the server. If the server is installed in a different location, modify the pathname accordingly.

The service-installation command does not actually start `mysqld`. Instead, it causes `mysqld` to run automatically whenever Windows starts. If you prefer to use a service that does not run automatically, install the server as a “manual” service:

```
C:\> C:\mysql\bin\mysqld --install-manual
```

As a general rule, when you install a server as a Windows service, you give no other options on the command line and list them in an option file instead. (See Section 12.2.3, “Specifying Server Startup Options.”) However, it is possible to specify a service name and option file as arguments, as described in the following discussion. This is especially useful when you install several Windows servers as services. (See Section 12.10, “Running Multiple Servers.”)
