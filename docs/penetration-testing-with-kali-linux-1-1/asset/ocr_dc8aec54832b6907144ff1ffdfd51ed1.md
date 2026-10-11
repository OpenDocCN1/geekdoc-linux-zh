```
```
total 36K
-rwxr-xr-x 1 kali kali 28K Jan 27 04:04 exploit
```
```

Listing 590 – Compiling the exploit from the local Exploit Database archive on Linux using gcc

After compiling the exploit on our target machine, we can run it and use whoami to check our privilege level:

![](bbox=[0.11, 0.21, 0.89, 0.7])

Figure 293: Elevating privileges on Linux through a privilege escalation exploit

Figure 293 shows that our privileges were successfully elevated from n00b (standard user) to root, the highest privilege account on Linux operating systems.

# ### 18.4 Wrapping Up

In this module, we have covered the concept of privilege escalation on both Windows and Linux operating systems as well as different architectures. We covered both manual and automated enumeration techniques that reveal required information for these types of attacks. In addition, we demonstrated the compilation process for both operating systems, demonstrated several privilege