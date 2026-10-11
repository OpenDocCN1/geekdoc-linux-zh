# Use Postfix Tools

Apart from the previously mentioned tools, Postfix also has a whole range of other useful administration tools that can make life considerably easier for a postmaster.

This section briefly introduces the administration tools for Postfix:

+   - **newaliases**. Converts the ASCII file `/etc/aliases` to the hash table `/etc/aliases.db`.

+   - **mailq**. Lists all emails in the mail queues that have not yet been sent.

+   - **postalias**. Converts the ASCII file `/etc/aliases` to the hash table `/etc/aliases.db`. Same as **newaliases**.

+   - **postcat**. Displays the contents of a file from the queue directories in a readable form.

+   - **postconf**. Without any parameters, this tool displays the values of all variables defined in the file `/etc/postfix/main.cf` as well as the values used by the standard variables. To modify variables directly, enter
+     `postconf -e key=value`
+   These changes are automatically integrated in the file `main.cf`.

+   - **postdrop**. This is run automatically by using the `sendmail` command, if `sendmail` cannot write any files to the maildrop directory because of missing world-writable permissions. It saves the forwarded email as `sgid maildrop`.

+   - **postfix**. Enables configuration errors to be found (**postfix check**), forces email from the deferred queue to be delivered immediately (**postfix flush**), or rereads the Postfix configuration files (**postfix reload**).

+   - **postmap**. Generates the hash tables for the lookup tables in the directory `/etc/postfix/`.