# APPLY YOUR KNOWLEDGE

20. Which of the following commands adds the printer luna to the class roughdrafts?

A. lpadmin -p luna -c roughdrafts
B. lpadmin -class roughdrafts -p luna
C. lpadmin luna -c roughdrafts
D. lpadmin -cp roughdrafts luna

21. Which of the following commands displays the characteristics of the printer hplaser?

A. lpstat -p hplaser -l
B. lpstat -p hplaser
C. lpadmin -p hplaser -l
D. lpstat -a -p hplaser -l

22. Which of the following commands changes a print request with the request ID eps1-29 to priority level 1?

A. lp -i eps1-29 -q 1
B. lpadmin -i eps1 -q 0
C. lp -i eps1-29 -q 39
D. lpadmin -i eps1 -q 39

# Answers to Review Questions

1. B. The UNIX utility responsible for printing in SRV4 UNIX is called lp.

2. B. For Solaris, the spool directory is located in /var/lp/spool.

3. C. The reject command disables any further requests for a printer or class entering the spooling area.

4. A., B., C. Use one of the following tools to add a local printer to a print server: Admintool, Printer Manager, or lpadmin.

5. B. The lpshut command stops the print service.

6. D. The lp command places information to be printed into the spooler.

7. A., C. A print server is a system that has a local printer connected to it. A print server makes a printer available to other systems on the network.

8. B., C. If the user doesn’t specify a printer name or class in a valid style, the command checks the user’s PRINTER or LPDEST environment variable for a default printer name.

9. A. When using Admintool to add a printer, the Print Server field defines the name of the system to which the printer is connected.

10. C. /dev/term/a is the serial port device.

11. B., C. Valid printer ports on a Solaris system include /dev/term/a, /dev/term/b, and /dev/ecpp0.

12. C. The following command cancels all print requests for the user bcalkins on the printer named jetprint:

`cancel -u bcalkins jetprint`

13. A., C. To delete a printer from the system, you can use either the lpadmin -x command or the Admintool interface.

14. B. Use the cancel command to remove a job from the print queue.

15. A. The print scheduler, lpsched, handles print requests on print servers.