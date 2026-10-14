The receiving of messages is no more involved, depending on what you want to do. To simply retrieve all of your messages, you can execute the following:

```
```bash
gnokii --getsms ME 1 end
```
```

This writes every SMS from your internal phone memory to the screen, where it could also be redirected into a file or parsed. There is a built-in parser, which will format text messages into that of an e-mail and append it in your inbox.

```
```bash
gnokii --getsms ME 1 end -a /var/mail/steev
```
```

Because this is an issued command, using received messages to control home devices takes a little work but is feasible, as you need to poll the phone periodically. An implementation would first require you need to keep a count of the messages you have in the inbox. This is not directly available, as the command reports all messages from every inbox:

```
```text
$ gnokii --showsmsfolderstatus
GNOKII Version 0.6.26
No. Name                         Id #Msg
========================================
  0 Internal memory             ME   92
  1 SIM card                    SM    0
```
```

However, because we’d be parsing each message anyway, it isn’t any more difficult and doesn’t matter that you might also download the same message you sent out previously. So, you get the number of total messages, like this:

```
```perl
#!/usr/bin/perl

my $status = `gnokii --showsmsfolderstatus 2>/dev/null`;
$status=~/ME\s+(\d+)/;
my $count=$1;
```
```

After retrieving the last total (held in whatever temporary or log file you decide to use), you can recall only the new messages and then process them accordingly:

```
```perl
for(my $msg=$lastCount;$msg<$count;++$msg) {
    my $txt = `gnokii --getsms ME $msg 2>/dev/null`;
    if ($txt=~/Inbox Message/) {
        $txt=~/Date\/Time\:(.*?)\n.*?Sender\:(.*?)Msg.*?\n.*?Text\:\n(.*)/;

        my $date = $1;
        my $sender = $2;
        my $message = $3;

        # process here...
    }
}
```
```