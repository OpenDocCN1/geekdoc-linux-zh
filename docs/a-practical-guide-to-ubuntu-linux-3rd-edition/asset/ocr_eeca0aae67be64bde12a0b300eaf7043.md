# # SOLVING A PROBLEM

Following is a list of steps that can help you solve a problem without asking someone for help. Depending on your understanding of and experience with the hardware and software involved, these steps may lead to a solution.

+   1. Ubuntu Linux comes with extensive documentation. Read the documentation on the specific hardware or software you are having a problem with. If it is a GNU product, use info; otherwise, use man to find local information. Also look in /usr/share/doc for documentation on specific tools. For more information refer to “Where to Find Documentation” on page 136.
+   2. When the problem involves some type of error or other message, use a search engine, such as Google (www.google.com/linux) or Google Groups (groups.google.com), to look up the message on the Internet. If the message is long, pick a unique part of the message to search for; 10 to 20 characters should be enough. Enclose the search string within double quotation marks. See “Using the Internet to Get Help” on page 143 for an example of this kind of search.
+   3. Check whether the Linux Documentation Project (www.tldp.org) has a HOWTO or mini-HOWTO on the subject in question. Search its site for keywords that relate directly to the product and problem. Read the FAQs.
+   4. See Table B-1 for other sources of documentation.
+   5. Use Google or Google Groups to search on keywords that relate directly to the product and problem.
+   6. When all else fails (or perhaps before you try anything else), examine the system logs in /var/log. First look at the end of the messages file using the following command:
+   
+   		$ sudo tail -20 /var/log/messages
+   
+   	If messages contains nothing useful, run the following command. It displays the names of the log files in chronological order, with the most recently modified files appearing at the bottom of the list:
+   
+   		$ ls -ltr /var/log
+   
+   	Look at the files at the bottom of the list first. If the problem involves a network connection, review the auth.log file on the local and remote systems. Also look at messages on the remote system.
+   7. The /var/spool directory contains subdirectories with useful information: cups holds the print queues, mail or exim4 holds the user's mail files, and so on.