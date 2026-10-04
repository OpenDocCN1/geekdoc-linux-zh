# ### Table 4-15: Attributes for the sendmail Tag

| Name | Function | Example |
| --- | --- | --- |
| mailhost | The Zoho MailHost object that manages data required to send electronic mail. If this attribute is used, the smthpost is unnecessary. | `<dt-sendmail mailhost="MailHost">` |
| smthpost | The address of the SMTP server to be used. If this attribute is used, the MailHost attribute is unnecessary. | `<dt-sendmail smthpost="mail.mycompany.com"> |
| port | This can be used only with the smthpost attribute, and the port number for a connection must be specified. If the smthpost attribute is used without the port attribute, the port number is set to 25 by default. | `<dt-sendmail smthpost="mail.mycompany.com" port="20">` |
| mailto | The recipient's address. Multiple addresses are separated by commas. | `<dt-sendmail mailhost="abc@beehive.com" mailto="xyz@mycompany.com">` |
| mailfrom | The sender's address. | `<dt-sendmail mailfrom="xyz@mycompany.com" subject="Meeting today">` |
| subject | The subject of the message. | |

![](bbox=[0.205, 0.495, 0.575, 0.775])

Figure 4-11: A simple email form