With such overwhelming capabilities, it’s easy to get lost within Metasploit. Fortunately, the framework is well-thought-out and offers a unified and sensible interface.

In this module, we will provide a walkthrough of the Metasploit Framework, including features and usage along with some explanation of its inner workings.

# ## 22.1 Metasploit User Interfaces and Setup

Although the Metasploit Framework is preinstalled in Kali Linux, the *postgresql* service that Metasploit depends on is neither active nor enabled at boot time. We can start the required service with the following command:

```
```
kali@kali:~$ sudo systemctl start postgresql

Listing 729 - Starting postgresql manually
```
```

Next, we can enable the service at boot with **systemctl** as follows:

```
```
kali@kali:~$ sudo systemctl enable postgresql

Listing 730 - Starting postgresql at boot
```
```

With the database started, we need to create and initialize the MSF database with **msfdb init** as shown below.

```
```
kali@kali:~$ sudo msfdb init
[+] Creating database user 'msf'
[+] Creating databases 'msf'
[+] Creating databases 'msf_test'
[+] Creating configuration file '/usr/share/metasploit-framework/config/database.yml'
[+] Creating initial database schema

Listing 731 - Creating the Metasploit database
```
```

Since Metasploit is under constant development, we should update it as often as possible. Within Kali, we can update Metasploit with **apt**.

```
```
kali@kali:~$ sudo apt update; sudo apt install metasploit-framework

Listing 732 - Updating the Metasploit Framework
```
```

We can launch the Metasploit command-line interface with **msfconsole**. The **-q** option hides the ASCII art banner and Metasploit Framework version output as shown in Listing 733.

```
```
kali@kali:~$ sudo msfconsole -q

msf5 > 

Listing 733 - Starting the Metasploit Framework
```
```

# ### 22.1.1 Getting Familiar with MSF Syntax

The Metasploit Framework includes several thousand modules, divided into categories. The categories are displayed on the splash screen summary but we can also view them with the **show -h** command.

```
```
msf5 > show -h
[*] Valid parameters for the "show" command are: all, encoders, nops, exploits, payload
s, auxiliary, post, plugins, info, options
```
```