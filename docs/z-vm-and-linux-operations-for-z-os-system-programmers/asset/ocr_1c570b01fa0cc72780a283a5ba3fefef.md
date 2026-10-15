# 5.1 Using a console to communicate to users

Section 2.7, "Consoles" on page 50 discusses the types of consoles that z/VM has available. Using these consoles allows communication to other z/VM users.

You can communicate with z/VM users by sending:

+   - General information messages to all logged-on users
+   - General information messages to a specific user
+   - Warning messages to all logged-on users
+   - Warning messages to a specific user

> z/OS analogy: z/OS users make use of the SEND command.

The MESSAGE and WARNING commands are limited by the length of the input command area. If the entire text of a message does not fit in this area, enter another command with the remaining text.

If an external security manager (ESM) is installed, you might not be authorized to use the MESSAGE or WARNING commands. However, messages sent to or from the system operator and messages sent with the ALL option are not subject to authorization checking by the ESM. For additional information, contact your security administrator.

If CP does not issue your message the way you entered it, it might be because you are including special line-editing symbols in the text of your message. For example, if logical line editing is in effect, the # symbol is your logical line-end symbol; if you include a # in your message text, CP cuts off your message. To prevent CP from interpreting these symbols as logical line-editing functions, enter the following command:

```
SET LINEDIT OFF
```

CP then issues your messages as you enter them.

# 5.1.1 Sending a general information message to all users

To send a general information message, such as "Query log for weekend schedule," to all logged-on users, enter:

```
message all query log for weekend schedule
```