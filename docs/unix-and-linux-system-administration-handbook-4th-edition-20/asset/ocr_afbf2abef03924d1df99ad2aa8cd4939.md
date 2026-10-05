# Chapter 22 Security

A common item you may want to configure is the list of files to ignore when doing file integrity (change) checking. For example, if you have a custom application that writes its log file to /var/log/customapp.log, you can add the following line to the <syscheckck> section of the file:

```
<syscheckck>
<ignore>/var/log/customapp.log</ignore>
</syscheckck>
```

After you've made this change and restarted the OSSEC server, OSSEC will stop alerting you every time the log changes. The new OSSEC configuration options are documented at ossec.net/main/manual/configuration-options.

It takes time and effort to get your HIDS system running. After a few weeks, you've filtered out the noise and the system will start to provide valuable information about changing conditions in your environment.

# 22.9 MANDATORY ACCESS CONTROL (MAC)

Mandatory Access Control is an alternative to the traditional UNIX access control system that controls of all permissions in the hands of a security administrator. In contrast to the standard model (described in Chapter 4, Access Control and Root Powers, and to some extent in Chapter 6, The Filesystem), MAC does not allow users to modify permissions, even on their own objects.

MAC security policies control access according to the perceived sensitivity of the resource being controlled. Users are assigned a security classification to a structured hierarchy. Users can read and write items at a higher classification level or cannot access items at a higher classification. For example, a user with "secret" can access and write "secret" objects but cannot read objects that are classified as "top secret."

A well-implemented MAC policy relies on the principle of least privilege (allowing access only when necessary), much as a properly designed firewall allows only specifically recognized services and clients to pass. MAC can prevent software with code execution vulnerabilities (e.g., buffer overflows) from compromising the system by limiting the scope of the breach to the few resources required by that software.

Needless to say, kernel modifications are necessary to implement MAC on UNIX and Linux. Our example UNIX systems (Solaris, HP-UX, and AIX) are all available in MAC-enabled versions at additional cost. These versions are called Solaris Trusted Extensions (formerly Trusted Solaris), HP-UX Security Containment, and Trusted AIX, respectively.

Unless you're handling sensitive data for a government entity, it is unlikely that you will ever need or encounter these security-enhanced editions.