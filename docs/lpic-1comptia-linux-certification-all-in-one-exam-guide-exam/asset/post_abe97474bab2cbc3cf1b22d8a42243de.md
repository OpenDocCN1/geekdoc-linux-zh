
## Accelerated Review

Most Linux distributions use CUPS to provide local and network printing.
The CUPS service is provided by the `cupsd` daemon.
CUPS can announce the availability of its printers on the local network.
Other Linux systems can listen for these announcements, connect to the CUPS service, and send print jobs to its printers.
The CUPS system is made up of the CUPS scheduler, CUPS filters, CUPS backends, PPD files, the web-based configuration utility, and the Print queue (`/var/spool/cups`).
The CUPS service is configured with the `/etc/cups/cupsd.conf` file.
To enable other Linux systems to print through your CUPS printers, you must uncomment the BrowseAddress directive in the `/etc/cups/cupsd.conf` file.
Use the `lpusers -g sys -a user_name` command at the shell prompt to create a CUPS administrative user.
You use the web-based configuration utility to configure your printers. It is accessed at http://localhost:631.
After creating your CUPS printer, you can send print jobs by selecting File | Print in a graphical Linux application.
You can send print jobs from the shell prompt using the `lp` command.
You can use the following command-line utilities to manage your CUPS system:
- `lprstat -t`
- `cancel`
- `lpoptions -d`
- `cupsaccept` / `cupsreject`
- `cupsenable` / `cupsdisable`

You can also manage Linux printing using the Line Printer Daemon (lpd).
You can use lpd commands to do the following:
- `lpr -P printer_name filename`
- `lpc status`
- `lpq`
- `lprm job_number`

You should use a standardized process to troubleshoot printing problems.
You should document the flow of print jobs to help you troubleshoot printing problems.
Commonly encountered printing problems include:
- Is the printer out of paper?
- Is the printer turned on?
- If it's a networked printer, is it connected to the network?
- Is the network up?
- Can you ping the printer from the user's workstation?
- Did the user select the correct printer when sending the print job?
- Has the correct printer driver been configured for the printer?

You can use the `hwclock` command to manage the hardware clock.
To synchronize time between networked Linux systems, you can use the `ntdate` command at the shell prompt.
The syntax is `ntdate time_server` where `time_server` is the IP address or DNS name of another Linux system on the network that is running the time service on UDP port 37.
After syncing the system time with `ntdate`, you may want to synchronize the system time with your hardware clock using the `hwclock --systohc` command.
A better way to keep time synchronized on a regular schedule is to use the Network Time Protocol (NTP).
NTP manages time in a much cleaner fashion than `ntdate`.
If there is a time differential between the time provider and the time consumer (your local system) it adjusts time gradually in small increments until time is eventually synchronized.
NTP is widely supported by most operating systems.
A system running `ntpd` can function as both a time consumer and a time provider at the same time.
The NTP protocol operates over IP port 123. The time consumer sends a time synchronization request to the time provider on port 123.
The time provider sends its time to the consumer, and the system time on the consumer is adjusted according to the NTP algorithm.
Several key NTP concepts that you need to be familiar with include the following:
- Stratum
- Stepping and slewing
- Insane time
- Drift
- Jitter

You can edit the `/etc/ntp.conf` file in a text editor to specify which system it should get time from.
The `pool.ntp.org` domain uses DNS round robin to make a random selection from a pool of time providers who have volunteered to be in the pool.
Before you actually start the `ntpd` daemon, you need to do a quick, one-time synchronization with your NTP time provider to avoid insane time issues by entering `ntpdate address_of_time_provider` at the shell prompt.
You can start the `ntpd` daemon using its init script in the appropriate init script directory used by your distribution.

E-mail messages are created and transferred using the MUA, MTA, and MDA as well as the IMAP or POP3 daemons.
Several commonly used Linux MTAs include the following:
- sendmail
- postfix
- qmail
- Exim

MTAs can’t download messages to e-mail clients via POP3 or IMAP.
To do this, you must install the `imap` package on your system.
You can use the `mail` command-line utility to read e-mail stored in the local MTA at the shell prompt.
To send a message, you can enter `mail recipient_address` at the shell prompt.
To view a list of unread messages in your mail queue, you can enter `mailq` at the shell prompt.

You can configure aliases for the MTA running on your Linux system.
Mail aliases redirect mail addressed to one user to another user’s account.
You use the `/etc/aliases` file to configure aliases.
This file defines one alias per line.
The alias you define must point to an existing e-mail address.
When done configuring aliases, you must run the `newaliases` command at the shell prompt as root to enable them.

You can also use the `.forward` file in your user’s home directory to configure forwarding.
Most Linux MTAs check for the existence of this file in the user’s home directory to configure forwarding of messages.
You can open/create the file in a text editor and enter the e-mail address to which you want to forward e-mail.

Two database services commonly implemented on Linux are:
- MySQL
- PostgreSQL

SQL defines statements that can be used to retrieve and update data in a database, such as SELECT, UPDATE, DELETE, INSERT, and WHERE.
A relational database is organized using fields, records, and tables.
A field is a single piece of information.
A record is one complete set of fields, and a table is a collection of records.
Each table is identified by a name, such as Customers.
Each table contains records (each one a single row) that contain one or more fields that in turn contain the actual database data.

You can use the following commands to manage data in an SQL database:
- SELECT
- UPDATE
- DELETE
- INSERT INTO
- CREATE TABLE
- ALTER TABLE
- DROP TABLE

You can use the `mysql` command at the shell prompt to connect to a MySQL database.
The syntax is `mysql -h host_name -u user_name -p`.
You can use the following commands within the `mysql` client:
- CREATE DATABASE
- USE
- SHOW TABLES
- CREATE TABLE
- DESCRIBE
- SELECT
- FROM
- WHERE
- DELETE
- UPDATE
- JOIN

## Questions

1. Which of the following commands will print two copies of the /home/tux/employees.txt file to a CUPS printer named MIN2300W?

A. lp -d MIN2300W -n 2 /home/tux/employees.txt
B. lp -p MIN2300W -c 2 /home/tux/employees.txt
C. lp /home/tux/employees.txt
D. lp -d MIN2300W /home/tux/employees.txt

2. Which of the following commands sets the default printer on a Linux system to a printer named MIN2300W?

A. lpoptions MIN2300W
B. lpstat -d MIN2300W
C. lp default = MIN2300W
D. lpoptions -d MIN2300W

3. Which CUPS component handles IPP printing requests from CUPS clients?

A. CUPS Scheduler
B. PDLs
C. CUPS Backends
D. PPDs

4. Your Linux system has an IP address of 192.168.1.20. What URL should you use in a browser to access the CUPS web-based administration utility?

A. http://192.168.1.20
B. https://192.168.1.20
C. http://192.168.1.20:631
D. http://192.168.1.20/cups

5. Which directive in the /etc/cups/cupsd.conf file specifies whether or not cupsd will announce its printers using broadcasts on the network?

A. BrowseAddress
B. BrowseAllow
C. Broadcast
D. Browsing

6. Which command can be used to set the hardware clock on a Linux system to the system time?

A. hwclock -w
B. hwclock -s
