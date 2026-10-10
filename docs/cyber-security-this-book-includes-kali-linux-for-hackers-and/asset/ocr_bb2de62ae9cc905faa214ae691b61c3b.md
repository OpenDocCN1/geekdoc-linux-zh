Some of these "exploits" can be downloaded from websites where repositories are maintained.

# The Metasploit Framework Console

http://www.metasploit.com/

The Metasploit Console (msfconsole) is mainly used to manage the Metasploit database, manage the sessions, as well as configure and execute the Metasploit modules. Its essential purpose is exploitation. This tool allows you to connect to the target so that the exploits can be executed against it.

Since the Metasploit Framework uses PostgreSQL as its database, it must be started in the first instance, and then start the Metasploit Framework console.

```
# service postgresql start
```

To verify that the service has started correctly, the following command must be executed.

```
# netstat -tna | grep 5432
```

To display the Metasploit Framework help.

```
# msfconsole -h
# msfconsole
```

Some of the useful commands to interact with the console are:

+   msf> help
+   msf> search [Module Name]
+   msf> use [Module Name]
+   msf> set [Option Name] [Module Name]
+   msf> exploit
+   msf> run
+   msf> exit

The following example details the use of the auxiliary module "SMB User Enumeration (SAM EnumUsers)".