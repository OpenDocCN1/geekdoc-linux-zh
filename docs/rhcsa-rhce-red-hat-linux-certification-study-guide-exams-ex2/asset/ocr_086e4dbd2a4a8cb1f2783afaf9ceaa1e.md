However, this may not be enough. If there's more than one instance of "Windows" in a line in the opsys file, it does not change the second instance of that word. But you can fix this by adding a "global" suffix:

```
# sed 's/Windows/Linux/g' opsys > newopsys
```

The following example would make sure that all Samba shares configured with the writable = yes directive are reversed:

```
# sed 's/writable = yes/writable = no/g' /etc/samba/smb.conf > ~/smb.conf
```

Of course, you should then review the results in the /root/smb.conf file before overwriting the original /etc/samba/smb.conf file.

# awk

The awk command, named for its developers (Aho, Weinberger, and Kernighan), is more of a database manipulation utility. It can identify lines with a keyword, and read out the text from a specified column in that line. A common example is with the /etc/passwd file. For example, the following command will read out the username of every user with a listing of "mike":

```
# awk '/mike/ {print $1}' /etc/passwd
```

# Edit Text Files at the Console

The original version of the RHCSA objectives specified the use of the vim editor. Strictly speaking, it doesn't matter what text editor you use to edit text files. However, I believe that you need to know how to use the vim editor, and apparently some at Red Hat agree. The vim editor is short for vi, improved. When installed, you can also start the vim editor with the vi command. Hereafter, I refer to that text editor as vi.

I believe every administrator needs at least a basic knowledge of vi. While emacs may be more popular and flexible, vi may help you save a broken system. If you ever have to restore a critical configuration file using emergency boot media, vi may be the only editor that you'll have available.

While RHEL 6 also includes access to the more intuitive nano editor, a knowledge of vi commands can help you identify key sections of man pages and other text files more quickly. While RHEL rescue media supports more console-based editors, I describe vi here simply because it's the editor I know best.