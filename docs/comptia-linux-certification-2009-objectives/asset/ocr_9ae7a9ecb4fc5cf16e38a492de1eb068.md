+   2.  Log in as root and verify that the job is complete.
    a.  At the **login** prompt, enter *root*
    b.  At the **Password** prompt, enter `p@ssw0rd`
    c.  Enter `vim nohup.out` to open the nohup.out file.
    d.  Observe that the file contains a listing of files and directories in the /etc directory, which indicates that the job is complete.
    e.  Press **Shift+G** to move to the end of the file.
    f.  Observe that the /etc/sysctl.conf file is the last entry listed.
    g.  Press `:` to switch to the command mode.
    h.  Enter `q` to close the file.
    i.  Enter `clear` to clear the terminal.