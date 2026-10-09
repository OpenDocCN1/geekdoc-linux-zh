+   3. Configure email aliases on the server labeled srvA.

+   a. Locate the “alias_maps = hash:/etc/aliases” directive.

+   b. The cursor is placed after `alias_maps = hash:`. To change the alias file location to `/postfix/aliases`, move the cursor to end of `/etc/`. Enter **postfix/**

+   c. Press **Esc** to switch to the command mode.

+   d. Locate the “alias_database = hash:/etc/aliases” directive.

+   e. The cursor is placed after `alias_database = hash:`. To change the alias file location to `/postfix/aliases`, move the cursor to the end of `/etc/`. Enter **postfix/**

+   f. Press **Esc** to switch to the command mode.

+   g. Save and close the file.

+   h. Using the **vi** editor, open the aliases file.

+   i. Enter **hr: chris, pat,**

+   j. Type **root: jsmith**

+   k. Press **Esc** to switch to the command mode.

+   l. Save and close the file.

+   m. Enter **postalias**  
**/etc/postfix/aliases** to update the aliases database file.

+   n. Start the postfix service.

+   o. Set the postfix service to run on booting the system.