# Attacking and Defending Oracle • Chapter 13

If you received this response, a vulnerability exists. Due to this use of the EXECUTE IMMEDIATE command, SCOTT can execute arbitrary SQL as the powerful SYS user by running this stored procedure. Needless to say EXECUTE IMMEDIATE can be dangerous if user input is not properly validated. It is strongly recommended that you revoke permissions using the following command:

```
REVOKE EXECUTE ON SYS.INITJMVUX FROM SCOTT;
```

Oracle comes with a plethora of ready-made PL/SQL packages but many of these have been “wrapped”. When a PL/SQL package has been wrapped using the wrap utility, its source code has been encrypted to prevent examination of the code. Many of the Oracle supplied packages are wrapped, which is slightly worrying. It makes the task of looking for vulnerabilities in these packages considerably harder. What exacerbates this problem is that the SPECIAL PUBLIC user can execute a large number of these wrapped and undocumented packages and procedures. I wonder how many issues are waiting there to be uncovered.

# PL/SQL External Procedures

PL/SQL packages can be extended to external functions in libraries or Dynamic Link Libraries. A developer would create a C function to perform whatever action is required and then compile this as a library. A PL/SQL package can then call this function. There are no special rules in terms of how to code the function or DLL, or such, any function in any library of the operating system can be executed. When a PL/SQL package is executing in the database server and it is required to execute such a C function, known as external procedures, Oracle connects to the Listener and the Listener load the relevant library, call the function, and pass any parameters passed to it. The Listener does not load the library into its own process space but rather launches another process extproc on Unix systems or extproc.exe on Windows platforms and directs Oracle to connect to it. Oracle obliges and named pipes and makes the same request that it made to the Listener. Extproc loads the library and calls the function (There is no authentication performed anywhere in this, and as will be seen later, it is actually possible for an attacker with no user ID and password to exploit this to break into the database server.)

To be able to call an external procedure from Oracle, a library must be created by a user that has one of the LIBRARY privileges. The LIBRARY PRIVILEGES include the following:

![](bbox=[0.707, 0.946, 0.927, 0.966])