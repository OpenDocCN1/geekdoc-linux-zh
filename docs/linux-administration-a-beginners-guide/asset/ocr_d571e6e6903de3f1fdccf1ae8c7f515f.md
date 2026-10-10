| Option Name | Description | Default |
| --- | --- | --- |
| confMAILER_NAME | The name used for internally generated mail (typically for error messages for returned mail). | MAILER-DAEMON |
| confDOMAIN_NAME | Your domain name. You should set this option only if Sendmail cannot determine your domain name by itself. | No default |
| confCW_FILE | The full path to the file containing host names that the server may be known as (see the use_cw_file feature). | /etc/sendmail.cw |
| confCT_FILE | The full path to the file containing trusted users (see the use_ct_file feature). | /etc/sendmail.ct |
| confCR_FILE | The full path to the relay-domains file. This is the list of domains Sendmail will relay for. (You should use the access_db feature instead.) | /etc/mail/relay-domains |
| confALIAS_WAIT | When the mail aliases file is updated, it must be converted to the internal database format with the newaliases command. This parameter tells Sendmail how long to wait for newaliases to run before rebuilding the database itself. | 10 minutes (10m) |
| confMIN_FREE_BLOCKS | The number of free blocks the mail storage partition must have for Sendmail to accept new messages. This option allows Sendmail to protect the system from sudden bursts of e-mail. | 100 blocks, where 1 block under Linux is equal to 1K |