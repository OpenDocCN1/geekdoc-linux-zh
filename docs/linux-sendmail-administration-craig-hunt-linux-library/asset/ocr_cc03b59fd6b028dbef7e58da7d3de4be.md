# Address Masquerading 251

```
> /try esmtp craig@wren.foobids.org
Trying header sender address craig@wren.foobids.org for mailer esmtp
canonify input: craig @wren . foobids . org
... Many lines deleted ...
final returns: craig@foobids.org
Rcode = 0, addr = craig@foobids.org
> /try esmtp craig@hawk.foobids.org
Trying header sender address craig@hawk.foobids.org for mailer esmtp
canonify input: craig @hawk . foobids . org
... Many lines deleted ...
final returns: craig@hawk . foobids.org
Rcode = 0, addr = craig@hawk.foobids.org
> /tryflags ES
> /try esmtp craig@wren.foobids.org
Trying envelope sender address craig@wren.foobids.org for mailer esmtp
canonify input: craig @wren . foobids . org
... Many lines deleted ...
final returns: craig @wren . foobids .org
Rcode = 0, addr = craig@wren.foobids.org
> ^D
```

Listing 9.3 is heavily edited to keep it to a reasonable length, but the key elements that show the default masquerading settings are. First, we display the contents of class w to show that it contains only four values; these are the four names that will be masquered. We use the /tryflags command to request processing for the header craig@wren.foobids.org for the esmtp mail. The address is rewritten to craig@foobids.org, showing that this configuration masquerades wren.foobids.org as foobids.org, in the header sender address. Next, we process craig@hawk.foobids.org as the header address for the esmtp mail. This time the address is not masquered. The reason is that hawk.foobids.org is not a value in class w. Finally, the address craig@wren.foobids.org is processed again. But this time, the /tryflags are set to request envelope sender (ES) processing. Even though the address is in class w, it is not masqueraded because it is an envelope address.

# Masquerade Options

The default settings of masquerading only header sender addresses and only for host identified in class w are usually adequate. In general, the purpose of masquerading addresses is to provide the correct reply address to the remote user. The user sees only the header addresses; the envelope addresses are used in the SMTP protocol exchanges. Thus, header masquerading is usually sufficient.