+   6. Check whether the mail message from junkmail.com is rejected.

a. Switch from the system labeled srvA to the system labeled srvB.

b. On the system labeled srvB, enter `telnet ourglobalcompany.com 25`

c. Enter `HELO ourglobalcompany.com`

d. Enter `MAIL FROM: junk@junkmail.com`

e. Enter `RCPT TO: chris@ourglobalcompany.com`

f. Observe that the error message, “451 4.3.5 Server configuration error”, is displayed indicating that the junk mail filter is working.

g. Quit the Telnet connection.

+   7. Check whether the recipient eric is denied access to receive mail messages.

a. On the system labeled srvB, enter `telnet ourglobalcompany.com 25`

b. Enter `HELO ourglobalcompany.com`

c. Enter `MAIL FROM: chris@ourglobalcompany.com`

d. Enter `RCPT TO: eric@ourglobalcompany.com`

e. Observe that the error message, “Recipient address rejected: Access denied,” is displayed.

f. Quit the Telnet connection.

g. Clear the terminal screen.