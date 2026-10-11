
You can then decide to promote print job *815* to the top of the queue with the following command:

```
lpc topq hplaser 815
```

This returns output similar to

```
Printer: hplaser@localhost
hplaser: selected 'root@localhost+815'
Kill server process PID 2795 with User defined signal 1
hplaser@localhost.localdomain: started
```

Then you can confirm that job *815* was sent to the top of the queue with this command:

```
lpq
```

This returns output similar to the following:

```
Printer: hplaser@localhost
Queue: 4 printable jobs
Server: pid 2795 active
Unspoiler: pid 2796 active
Status: waiting for subserver to exit at 09:03:08.971

Rank Owner/ID Class Job Files Size Time
1 root@localhost+815 A 815 /etc/printfcap 997 09:02:17
active root@localhost+794 A 794 /etc/printfcap 997 09:02:15
3 root@localhost+811 A 811 /etc/printfcap 997 09:02:16
4 root@localhost+813 A 813 /etc/printfcap 997 09:02:17
```

As you can see, the command did promote job *815* to the top of the queue, as requested. Use this for emergency print jobs, to get little memos out before 500-page PDF files, and so on.

# Additional Printing Commands

Several other commands don't really come with the lpd suite but are present for use when printing. The following lists some commands that are likely to appear on the exam and that you can use in real life:

- `mpage`—The `mpage` command is used for printing multiple print pages per sheet of paper when using PostScript printers.
- `lp`—The `lp` command is used with later versions or variations of the `lpd` daemon, notably the LPRNG printing suite. `lp` is normally a symbolic link back to the `lpr` command and is used most often by homesick Solaris sysadmins.
- `lpstat`—If you see the `lpstat`, `lpinfo`, or `lprm` command on the exam, they are being used by the exam writers as a distractor, or incorrect answer. These commands aren't used by **`lpd`** and are often on the system as symlinks made by a sysadmin.

![](img/49f4f38f3aec011238fa50f89e643db3_443_0.png)

Watch for the commands associated with the **`lpd`** daemon versus ones for the **`lp`** printing service on System V machine Unix versions, such as Solaris and AIX. Only **`lpd`** commands or links to them are correct answers on the exam.

# Printer Security

The last exam-related situation that needs coverage for printing is security for print jobs or the ability to print. This is accomplished in two methods—either putting a group ownership on the spool directory or by limiting the printing capability by the host submitting the print job.

By default, all hosts on your network can print to any printer, but by setting the parameters and entries in the `/etc/hosts.lpd` file, you can control who can and cannot print to a server’s printers.

![](img/49f4f38f3aec011238fa50f89e643db3_443_1.png)

To clarify, if you need to print to a remote host that restricts printer usage via the `/etc/hosts.lpd` file, your hostname must be added to that file to allow your host’s processes to print to the remote host’s printers.

The `/etc/hosts.lpd` file is very simple. The typical entry in the file is either an unqualified hostname or a fully qualified domain name, the presence of which means that the host is allowed to print on that server’s printers.

An example of a functional `/etc/hosts.lpd` file is as follows:

```
bruce.example.com
geddy.example.com
zakk.example.com
192.168.1.201
```

In the file shown here, only the listed hosts can submit print jobs across the network to this host’s printers. The `/etc/hosts.lpd` file allows hostnames or IPs.

![](img/49f4f38f3aec011238fa50f89e643db3_443_2.png)

Watch for the missing step in a printer configuration on the exam. If the printcap file `(/etc/printcap)` is correctly configured and the host still can’t print to a remote server, you need to add an entry for the printing host to the remote server’s `/etc/hosts.lpd` file.

# Exam Prep Questions

1. You are configuring a user’s printer settings for a remote server. Which parameter should be present in the `/etc/printcap` printer definition to successfully deliver print jobs to a remote host? (Choose two.)
   - A. `remote=`
   - B. `rpm=`
   - C. `rp=`
   - D. `rmc=`
   - E. `rm=`
   
   Answers C and E are correct because the `rm=hostname` and `rp=printername` parameters are needed for sending remote print jobs. Answers A, B, and D are incorrect because no options by those names exist in the `/etc/printcap` file specification.

2. You need to allow a host named `ishmael` in your local domain to print on your host’s `lpd` daemon print queues. In the blank below, enter the exact syntax that will allow printing for this host, if put in the `/etc/hosts.lpd` file:
   ______
   
   The correct answer is **ishmael**. There are no correct alternative answers.

3. Which of the following command lines promotes all print jobs on the queue `brother` that belong to the user `llaffer` to the top of the queue?
   - A. `lpc -P brother topq llaffer`
   - B. `lpc topq brother llaffer`
   - C. `lpc brother topq llaffer`
   - D. `lpc topq -Pbrother llaffer`
   
   Answer B is correct because the `lpc` command’s `topq` option syntax is `lpc topq printer user`. Answer A is incorrect because `lpc` doesn’t use the `-P printer` syntax and the order is incorrect. Answer C is incorrect because the `topq` option must be used before the printer name. Answer D is incorrect because neither the `-Pprinter` nor `-P printer` syntax works with `lpc`.

4. Which file on a remote host should be configured to allow your host to print to its already functioning printers? Fill in the blank below with the full path and filename of the appropriate file:
   ______
   
   The correct answer is **/etc/hosts.lpd**. There are no correct alternative answers.

5. Which command prints two copies of the file to the default printer? (Choose all that apply.)
   - A. `cat hosts ; lpr -#2`
   - B. `for 1 in 2 lpr > hosts`
   - C. `lpr -P -count 2 hosts`
   - D. `cat hosts > lpr ; cat hosts > lpr`
   - E. `lpr -K2 hosts`
   
   Answers A and E are correct because only the `-#` and `-k` options are capable of printing multiple copies from `lpr`. Answer B is incorrect because, even though the loop might work, you can't print with this command because you get either a syntax error or a continuation prompt waiting for more input. Answer C is incorrect because there isn't any such parameter for `lpr`. Answer D is incorrect because it only sends (twice) the contents of the `hosts` file to a file named `lpr` in the local directory and does not print the `hosts` file.

6. Which command with any options, keywords, or parameters removes just the first queued print jobs on all print queues but does not remove multiple print jobs from any of the queues? Fill in the blank below with the exact command string that accomplishes this task:
   ______
   
   The correct answer is `lprm -a`. There are no correct alternative answers.

7. What is the full path and filename of the spool directory for the printer `hplaser` on a system that uses the standard `lpd` printing daemon and the default locations?
   - A. `/usr/spool/lpd/hplaser`
   - B. `/var/spool/lphplaser`
   - C. `/var/spool/lpd/1p`
   - D. `/var/spool/lpd/hplaser`
   
   Answer D is correct because the `lpd` daemon default base directory for printer spools is `/var/spool/lpd` and you just have to add the printer name to complete the answer. Answer A is incorrect because the default base for the spool directory isn't in the `/usr` tree. Answer B is incorrect because the base directory is `/var/spool/lpd`. Answer C is incorrect because the name of the printer is `hplaser` and there is no indication in the question that it is named `1p`, even though that might be an alias for the printer.

8. Which of the following is true about the standard `lpd` daemon and its associated processes on a default system? (Choose all that apply.)
   - A. `lpd` uses a single instance for all defined printers.
   - B. `lpd` uses one subprocess for each printer defined.
   - C. `lpd` jobs are sent directly to the print device.
   - D. `lpd` uses the `/etc/hosts.lpd` for printer definitions.
   - E. `lpd` conforms to the BSD style of printing.
   
   Answers B and E are correct because the `lpd` daemon uses a subprocess for each defined printer and follows the BSD style of printing. Answer A is incorrect because the `lpd` daemon uses multiple subprocesses, one per defined printer. Answer C is incorrect because `lpd` print jobs are sent to the spool directory and then are sent to the print device. Answer D is incorrect because `lpd` uses the `/etc/hosts.lpd` file for printing security and the `/etc/printcap` file for printer definitions.

9. Which of the following commands prints the file `space.kl` on the printer `hplaser`? (Choose all that apply.)
   - A. `lpr -P hplaser -F space.kl`
   - B. `lpr -Phplaser space.kl`
   - C. `lpc printer=hplaser file=space.kl`
   - D. `lpr -p hplaser space.kl`
   - E. `lpr -P hplaser space.kl`
   
   Answers B and E are correct because the `-P` option can be followed either directly by the printer name or a space and then the printer name. Answer A is incorrect because there should not be a `-F` parameter in the `lpr` command line. Answer C is incorrect because the `lpc` command does not submit print jobs. Answer D is incorrect because there must be a capital P, not a lowercase p, in the printer name option.

10. Which command, with any needed options and parameters, shows you the most information about the default `lpd` print queue without using the debugging options? Fill in the blank below with the appropriate command:
    ______
    
    The correct answer is `lpq -l`. There are no correct alternative answers.

11. If your system is using the BSD style of printing and has two printers defined and active, you will see multiple instances of the daemon or service running. Fill in the blank below with just the daemon name:
    ______
    
    The correct answer is `lpd`. There are no correct alternative answers.
