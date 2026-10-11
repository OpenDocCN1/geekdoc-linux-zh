# ## 18. Privilege Escalation

During a penetration test, we often gain an initial foothold on a system as a standard or non-privileged user. In these cases, we generally seek to gain additional access rights before we can demonstrate the full impact of the compromise. This process is referred to as Privilege escalation and it is a necessary skill as "direct-to-root" compromises are arguably rare in modern environments.

In this module, we will assume we have gained non-privileged user access on a Windows and Linux-based target and will demonstrate privilege escalation techniques on those targets.

While every target can be considered unique due to differences in OS versions, patching levels, and various other factors, there are some common escalation approaches. To leverage these, we will search for misconfigured services, insufficient file permission restrictions on binaries or services, direct kernel vulnerabilities, vulnerable software running with high privileges, sensitive information stored on local files, registry settings that always elevate privileges before executing a binary, installation scripts that may contain hard coded credentials, and many others.

# ### 18.1 Information Gathering

After compromising a target and gaining the initial foothold as an unprivileged user, our first step is to gather as much information about our target as possible. This allows us to get a better understanding of the nature of the compromised machine and discover possible avenues for privilege escalation.

In this section, we will explore both manual⁴³⁹⁴⁴⁰ and automated information gathering and enumeration techniques and discuss the strengths and weaknesses of each.

# #### 18.1.1 Manual Enumeration

Manually enumerating a system can be time consuming. However, this approach allows for more control and can help identify more exotic privilege escalation methods that are often missed by automated tools.

Some of the commands in this module may require minor modifications depending on the versions of the target operating system. In addition, not all the commands presented in this section will be replicable on the dedicated clients.

# ##### 18.1.1.1 Enumerating Users

When gaining initial access to a target, one of the first things we should identify is the user context. The whoami command, available on both Windows and Linux platforms, is a good place to start.

+   ⁴³⁹ (G0tm1k, 2011). https://blog.g0tm1k.com/2011/08/basic-linux-privilege-escalation/
+   ⁴⁴⁰ (FuzzySecurity, 2014). https://www.fuzzysecurity.com/tutorials/16.html