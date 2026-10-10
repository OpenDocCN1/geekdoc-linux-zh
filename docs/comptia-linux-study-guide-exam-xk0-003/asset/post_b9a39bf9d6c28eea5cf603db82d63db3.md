
such rules combine together to create a complete firewall. Typically, a script runs at system startup to manage this task.

- **Describe common text-mode remote login tools.** Telnet was the traditional text-mode login tool, but it passes data over the network unencrypted and so is a poor choice today. The Secure Shell (SSH) is the most common remote text-mode access tool today.
- **Explain the nature of X clients and servers.** An X server controls a screen display and handles input from the user’s mouse and keyboard. Therefore, the X server is used directly by the user, and X clients are the programs that rely on the X server’s services.
- **Explain the role of an XDMCP server.** An XDMCP server, such as XDM, KDM, or GDM, launches X and controls access to X via a login prompt—that is, it serves as Linux’s GUI login system. XDMCP servers are also network enabled, providing a way to log in remotely from another X server.
- **Explain the role of Ghostscript in Linux printing.** PostScript is the standard Linux printing language, and Ghostscript converts PostScript into bitmap formats that are acceptable to non-PostScript printers. Thus, Ghostscript is a critical translation step in most Linux print queues.
- **Summarize how print jobs are submitted and managed under Linux.** You use `lpr` or `lp` to submit a print job for printing, or an application program may call `lpr` or `lp` itself or implement its functionality directly. The `lpq` or `lpstat` utility summarizes jobs in a queue, and `lprm` can remove print jobs from a queue.

## Review Questions

- 1. What is the default port used by the Simple Mail Transfer Protocol (SMTP)?
    - A. 143
    - B. 80
    - C. 25
    - D. 21

- 2. Which of the following ports are known as *unprivileged* ports?
    - A. Those that have numbers above 1024
    - B. Those that have numbers between 512 and 1024
    - C. Those that have numbers between 1 and 100
    - D. Those that have numbers below 1024

- 3. Which port, by default, is commonly used by OpenSSH?
    - A. 20
    - B. 21
    - C. 22
    - D. 23

- 4. Which port, by default, is commonly used by HTTPS?
    - A. 111
    - B. 143
    - C. 389
    - D. 443

- 5. Which of the following is true of the DROP policy for `iptables`?
    - A. It replies as if the computer was available but running no software on the target port.
    - B. It ignores packets, providing the illusion of a network error between the sender and recipient.
    - C. It may be used only on ports that are opened by servers, not clients.
    - D. It may be applied as a default policy but not on a port-by-port basis.

- 6. When is it reasonable to enable routing between network segments on a computer that's connected to both of them?
    - A. Whenever one of the network segments is connected to the Internet and the other segment is a private network.
    - B. Whenever the segments must communicate directly and the computer in question is configured as a firewall.
    - C. Whenever the segments must communicate directly and the computer in question is designated as the router.
    - D. Never; this task should be handled only by dedicated network hardware that never runs Linux.

- 7. A firewall script includes the following two lines. What is their purpose?
    ```bash
    iptables -A OUTPUT -d 127.0.0.1 -o lo -j ACCEPT
    iptables -A INPUT -s 127.0.0.1 -i lo -j ACCEPT
    ```
    - A. To set the default policy for all chains to ACCEPT; subsequent rules will use DROP or REJECT.
    - B. To enable routing of localhost traffic on a computer configured as a router.
    - C. To enable communications over the localhost interface for local programs.
    - D. To set the default policy for the OUTPUT and INPUT chains to ACCEPT, leaving the FORWARD chain unaffected.

- 8. Broadly speaking, how will use of `iptables` on a router with firewall features differ from its use on a workstation?
    - A. A router's `iptables` rules will include an emphasis on the FORWARD chain; a workstation's will emphasize the INPUT and OUTPUT chains.
    - B. A router's `iptables` rules will most likely use a default DROP policy, whereas a workstation's will probably use a default ACCEPT policy.
    - C. A router's `iptables` rules will be activated by a script, whereas a workstation's will be configured using a GUI tool.
    - D. A router's `iptables` rules will emphasize privileged port numbers, whereas a workstation's will emphasize unprivileged port numbers.

- 9. You want to use an X server on an old Pentium computer to run X clients on a modern Itanium CPU system, with the goal of performing computationally intensive spreadsheet calculations. Which of the following is true?
    - A. The spreadsheet will compute slowly because of the slow speed of the Pentium server.
    - B. You won't be able to run the spreadsheet because the Itanium and Pentium CPUs need different executables.
    - C. The computation will run swiftly, but graphics displays may be slowed by the Pentium's limited speed.
    - D. Computations will run swiftly only if the Itanium computer makes its filesystem available via NFS.

- 10. Why is it unwise to allow root to log on directly using SSH?
    - A. Somebody with the **root** password but no other password could then break into the computer.
    - B. The **root** password should never be sent over a network connection; allowing **root** logins in this way is inviting disaster.
    - C. SSH stores all login information, including passwords, in a publicly readable file.
    - D. When logged on using SSH, **root**'s commands can be easily intercepted and duplicated by undesirable elements.

- 11. What programs directly support secure encrypted file transfers via SSH? (Choose all that apply.)
    - A. `ftp`
    - B. `sftp`
    - C. `scp`
    - D. NFS

- 12. What program can you use to generate a key that will enable logins to remote SSH servers without using a password?
    - A. `authorized_keys`
    - B. `ssh-keygen`
    - C. `sshpasswd`
    - D. `id_rsa`

- 13. To whom should you distribute your server's main SSH private key?
    - A. Only to servers with which you want to communicate
    - B. Only to servers that have already provided their own public keys
    - C. To anybody who can provide a matching SSH public key
    - D. None of the above

- 14. Which of the following is generally true of Linux programs that print?
    - A. They send data directly to the printer port.
    - B. They produce PostScript output for printing.
    - C. They include extensive collections of printer drivers.
    - D. They can print only with the help of add-on commercial programs.

- 15. Which of the following describes the function of a smart filter?
    - A. It detects the type of a file and passes it through programs to make it printable on a given model of printer.
    - B. It detects information in print jobs that might be confidential, as a measure against industrial espionage.
    - C. It sends e-mail to the person who submitted the print job, obviating the need to wait around the printer for a printout.
    - D. It detects and deletes prank print jobs that are likely to have been created by miscreants trying to waste your paper and ink.

- 16. What information about print jobs does the `lpq` command display? (Choose all that apply.)
    - A. The name of the application that submitted the job
    - B. A numerical job ID that can be used to manipulate the job
    - C. The amount of ink or toner left in the printer
    - D. The username of the person who submitted the job

- 17. You try to create a definition for a new printer using the CUPS Web-based tool, but you can't find a suitable printer definition. How might you proceed?
    - A. Edit the `/etc/cups/printers.conf` file directly.
    - B. Use the `system-config-printer` program instead of the CUPS Web tool.
    - C. Install the LPRng package, if it's not already installed.
    - D. Install the Foomatic package, if it's not already installed.

- 18. In setting up a network printer for use in Linux, a system administrator uses the following URI:
    ```
    smb://bsd:lpd@USB/PARALLEL
    ```
    Assuming this URI is correct, what type of printer is the administrator attempting to use?
    - A. A local parallel-port printer
    - B. A local USB printer
    - C. A networked Windows or Samba printer
    - D. A networked BSD LPD printer

- 19. You type `lpr -P brother sample.ps` file to submit a print job. What would you type to do the same thing using `lp`?
    - A. `lp -d brother sample.ps`
    - B. `lp -p brother sample.ps`
    - C. `lp --printer brother sample.ps`
    - D. `lp -P brother sample.ps`

- 20. Under what circumstances may ordinary users cancel other users' print jobs on a system that uses CUPS?
    - A. Only if the print queue has registered an error condition (paper out, printer jam, and so on)
    - B. Only if the administrator has enabled the option to allow this activity
    - C. Only if permissions on the original file or its directory permit other users to delete the file
    - D. Never
