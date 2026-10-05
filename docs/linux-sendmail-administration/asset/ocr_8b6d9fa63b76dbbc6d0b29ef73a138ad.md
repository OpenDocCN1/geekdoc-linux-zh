# Table A.3 OSTYPE Defines (continued)

| Parameter | Function |
| --- | --- |
| SMTP_MAIL_MAXMSG | The maximum number of SMTP messages delivered by a single connection. |
| STATUS_FILE | Name of the status file. [/etc/mail/statistics] |
| USENET_MAILER_ARGS | Arguments for the Usenet mailer. [-m -h -n] |
| USENET_MAILER_FLAGS | Usenet mailer flags. [rsDFMn] |
| USENET_MAILER_MAX | Maximum size of Usenet messages. [100000] |
| USENET_MAILER_PATH | Program used for news. [/usr/lib/news/inews] |
| UCPP_MAILER_ARGS | UCPP mailer arguments. [uux -r -z -a5g -gC $h!mail ($u)] |
| UCPP_MAILER_CHARSET | Character set for UCPP 8-bit MIME mail. |
| UCPP_MAILER_FLAGS | Flags added to DFmU for the UCPP mailer. |
| UCPP_MAILER_MAX | Maximum size for UCPP messages. [100000] |
| UCPP_MAILER_PATH | Path to the UCPP mail program. [/usr/bin/uux] |

The essential characteristic of the items in Table A.3 is that all have something to do with the location of files on the system. Some of these, as HELP_FILE, STATUS_FILE, ALIAS_FILE, and QUEUE_FILE, are obviously file locations. The others, all of which relate to mailers, might not be so obviously linked to file locations unless you realize that most of the mailers require a pathname. If some mailer options are going to be placed in the OSTYPE source file, it only makes sense to put all of them here. Because files vary from system to system, it is traditional to put file locations and mailer options in the OSTYPE source file.

The MODFY_MAILER_FLAGS macro can be used to change the flags of a mailer. This is slightly different than the mailer flags definitions covered in Table A.3. All of those definitions can add flags, but none of them can remove a flag that is already defined. For example:

```
define(`LOCAL_MAILER_FLAGS`, `9`)
```