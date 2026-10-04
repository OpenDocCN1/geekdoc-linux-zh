
# Attacking and Defending Oracle • Chapter 13

By issuing the services or status command, one can tell what operating system the server is running on and what services are offered and on what TCP port. This is information that the Listener should not leak. The real issue is with setting the location of the log files. For example, it is possible to set the log file to the listener.ora configuration file and add entries to it by making certain crafted requests. By doing this, one can cause the Listener to run arbitrary programs when the Listener restarts. Attackers can perform further attacks by writing files that are normally executed by the operating system, such as the autoexec.bat file on a Windows system. It is highly important that the Listener be secured. See the section entitled "Securing the Listener" for more details.

# External Procedure Services

A particularly serious issue exists in which the external procedure, or extproc, service be manipulated to load and call arbitrary dynamic link libraries (DLLs) on the operating system. This results because extproc requires no authentication. This allows an unauthenticated user to gain full control over the database or possibly the operating system.

This vulnerability is exposed through a feature of Procedural Language/Structured Query Language (PL/SQL) packages that allows them to call external functions in libraries or Dynamic Link Libraries (for more information about PL/SQL packages, see the "Attacking the Database" section). When a PL/SQL package attempts to call an external procedure, the Oracle process connects to the Listener and requests that the Listener load the relevant library, call the function, and pass the function list of parameters. The Listener does not load the library into its own process address but rather another extproc process (on Unix systems) or extproc.exe (on Windows platforms) and directs Oracle to connect to it. Oracle obliges the extproc process, and makes the same request that it makes to the Listener. Extproc loads the library and calls the function. The extproc communication protocol. There is no authentication performed anywhere throughout this process. This opens a gaping and extremely dangerous security hole. See Figure 13.2.

Because of the lack of authentication in the extproc service, an attacker can masquerade as an Oracle process and execute any function in any DLL on the file system. This problem is exacerbated by the fact that this can be exploited remotely; because of this, an attacker can write a script that connects to the Listener/extproc over Transmission Control Protocol (TCP), and without having to authenticate, can run any function in any library he wishes. A real-world attack would probably call the function system() exported by msvcrt.dll all

![](img/729efc56f204a2ebffb8295c3a2dfdfb_709_0.png)

Windows platforms or exe() or system() exported by libc on Unix platforms. Any operating system command passed as a parameter to these functions would run in the security context of the account running the Oracle processes. On Unix systems, and on Windows NT/2000 this is, by default, the local SYSTEM account. Any commands executed as these users will have dire consequences for the targeted computer system. Several things can be done to mitigate the risk of such an attack. The first line of defense is, of course, with the use of a firewall. No one should be able to access the Listener port of TCP 1521 from the Internet. This not only helps risk concerned with this problem but few others. Provided the Web server has been secured, there should be minimal risk of an attacker originating from the Web server. Please see the "Securing the Listener" section later in the chapter for more details.

# Figure 13.2 Extproc Communication

| Standard extproc usage | Malicious extproc usage |
|---|---|
| Step 2 - Listener executes the extproc.exe file and passes the DLL as a parameter | Extproc.exe | Step 2 - Listener executes the extproc.exe file and requests to load msvcrt.dll | Extproc.exe |
| Listener on port 151 | Step 1 - Attacker sends a request to the listener to execute extproc.exe and load the DLL msvcrt.dll | Listener on port 151 |
| Step 1 - Database requests listener to start an extproc engine and load a specific DLL | Database SID=ord | Step 3 - Extproc loads msvcrt.dll and run system() with malicious command | Client | Database SID=ord |

Version 9.0.1.3.1 of Oracle is still vulnerable to this problem, version 9.2.0.1.0 takes steps to prevent an attacker from exploiting this. It does this in two ways: first, only libraries found in the ORACLE_HOME\bin directory can be loaded; and second, only connections coming from the local machine will be honored. There are still few problems with this, however. A remote attacker can still connect to extproc over TCP/IP and make the same request. Extproc will not service the request and will write out an error to log file stating that an attempt was made to load a library from a remote machine.

# Attacking and Defending Oracle • Chapter 13

Although the intention is good, the implementation of this fix introduces another problem—a buffer overflow vulnerability exists in extproc. The name of the library is written to the log file, and if the attacker supplies a sufficiently long filename, a return address is overwritten on the stack, the attacker can gain control to run arbitrary code anyway. As a further note, a local attacker can still do a vast of nefarious things even if she is limited to loading libraries in the binary. This directory has 32 DLLs on a Windows—any number of exported functions can be abused to gain control of the system.

This buffer overflow in extproc was discovered by Chris Anley, a co-founder of NGSSoftware, in late 2002. Oracle has been informed of the problem, and we are working on a patch, which should be available early 2003. Once the patch is available, you can likely find more information about the vulnerability and the path on /otn.oracle.com/deploy/security/alerts.html.

# Denial of Service When Redirection Occurs

The Listener service also has problems with denial of service attacks. When the Listener hands off connections to the database instance by redirecting the connection to an alternate port, a denial of service attack can prevent the Listener from accepting new connection attempts and possibly crash the service.

The vulnerability exists because the database creates a new thread each time a request is made by a user. An attacker can simply make 1,500 requests to connect to the database, and the Listener will request the database instance to create 1,500 new threads. The database will happily sit and wait on these new threads until a connection is made. The problem is that after opening 1,500 new threads, the database will fail to open additional threads and more likely you will have consumed all the memory on the operating system. Once again, since the redirection occurs before an authentication occurs, this attack can be mounted by anyone to send a TCP/IP packet to the Listener.

# Attacking the Database

Attacks on the database instance can occur both before authentication takes place and after a privileged user is connected. Unauthenticated attacks are usually higher profile because hackers are envisioned as people who cannot simply log in to the system with a username and password. Even when a vulnerability requires an attacker to connect to the database with a username and password, that’s not a problem for the attacker. When Oracle is installed, a large number of default accounts are created, and most of them have a password that is equal to their username. Oracle is infamous for this, and it can make the job of an attacker that much easier.

![](img/729efc56f204a2ebffb8295c3a2dfdfb_711_0.png)

A list of “default” user IDs and their passwords can be found on the Internet at sites such as www://pentest-limited.com/user-table-new.htm.

# Buffer Overflows in Authentication

The current version of Oracle, 9.2.0.1.0, suffers from a buffer overflow vulnerability that can be exploited with a valid username and password; this overrun occurs in the authentication process. By supplying an overly long username, a buffer overflow occurs and the exception handler can be overwritten on the stack, allowing an attacker to gain control of the Oracle Database Server. Once again, Oracle Corporation was alerted to this buffer overflow and is working on a patch, which is expected in early 2003. Once the patch is available, more information about the vulnerability and the patch will likely appear on http://utm.oracle.com/deploy/security/alerts.html.

# Buffer Overflows in SQL

If an attacker has a username and password, he can exploit a number of other buffer overflow vulnerabilities.

```
CREATE DATABASE LINK foobar
CONNECT TO blah LONG IDENTIFIED BY blah
USING 'LONG_LONG_STRING'
```

```
SELECT * from foo@foobar
```
