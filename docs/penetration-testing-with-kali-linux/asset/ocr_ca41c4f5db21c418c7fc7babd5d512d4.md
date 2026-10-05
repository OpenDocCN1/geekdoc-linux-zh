# Listing 679 - Migrate to process.exe

Listing 679 shows that we successfully migrated our process to the OneDrive process. When reviewing the process list, we will find our original process, met.exe with ID 2552, does not exist anymore. Furthermore, we'll notice that the ps output contains less information than before. The reason for this is that we are now running in the context of the process with the ID 8052 and therefore, as user offsec.

```
meterpreter > getuid
Server username: ITWK01@offsec
Listing 680 - Command execute as user offsec instead of NT AUTHORITY\SYSTEM
```

Instead of migrating to an existing process or a situation in which we can't find any processes to migrate to, we use the Meterpreter command. This command provides the ability to create a new process by specifying a command or program.

To demonstrate this, let's start a Notepad process and migrate to it as user offsec. For this, we use execute with -H to create the process from hidden and _notepad as argument for -f to specify the command or run to. Then, we are migrated to the newly spawned process. 

```
meterpreter > execute -H -f notepad
Process 2720 created.
```

```
meterpreter > migrate 2720
[+] Migrating from 8052 to 2720...
[+] Migration completed successfully.
```

> Listing 681 - Migrate to a newly spawned Notepad process

Listing 681 shows how we can migrate to the newly spawned Notepad process. Since we used the option -H, the notepad was spawned without any visual representation. However, the process is still listed in the process list of applications such as the task manager.

This concludes this section. We explored several post-exploitation features of Meterpreter. First, we used idtime to check if the user is actively working on the system or not. Next, we elevated our privileges with the help of getsystem. Finally, we migrated to move the execution of our Meterpreter payload to a different process.

> Meterpreter offers a variety of other interesting post-exploitation modules as hashdump, dumps the contents of the SAM database or screenshare, which displays the target machine's desktop in real-time.

While these Meterpreter features are quite powerful, Metasploit contains numerous modules that extend the basic post-exploitation features we explored in this section. We'll review and use some of them in the next section.