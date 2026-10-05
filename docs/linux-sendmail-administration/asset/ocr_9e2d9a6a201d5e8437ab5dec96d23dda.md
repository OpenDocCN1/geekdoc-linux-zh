# Simple Command-Line Options 277

Option, a single character indicates a special status for this piece of mail can follow the queue identifier. There are three possible single character values:

+   * indicates that the queue file containing the mail is locked by a valid file-locking mechanism.

+   * indicates that the MinQueueAge option has been set in the Sendmail configuration, and that piece of mail has not been queued long enough to meet the MinQueueAge requirement. The MinQueueAge sets the minimum amount of time a message must remain in the queue. It tells Sendmail not deliver messages that fall below this minimum when Sendmail processes the queue. By default, this option is commented out of the sendmail.cf file and Sendmail delivers all of the messages from the queue that it

+   X indicates that the load of the server is currently too high to deliver this piece of mail.

Size The second field contains the size of the mail message in bytes. In Listing 10.5, the message is 1190 bytes.

Q-Time The third field contains the date and the time that the message first entered the queue, displayed in a simple, straightforward manner.

Sender/Recipient At a minimum, the fourth field contains the address of the sender and the address of the recipient of this piece of mail. Usually, this field has more information than just the addresses. The field begins with the sender address. In Listing 10.5, the sender address is creat. This is followed by the MIME message body, if the message contains special MIME data. In Listing 10.5, no message body is listed, so it is a traditional text message in an RFC 822 format. After the message body is listed, mail1q displays the error message associated with the last delivery attempt in parentheses, if the queue file has a copy of the error message. In Listing 10.5 it is Deferred: goat.mammals.org : Network is unreachable. The fourth field ends with the recipient address, which in Listing 10.5 is sara@goat.mammals.org.

![](bbox=[0.933, 0.526, 0.986, 0.673])

The amount of information displayed by mail1q is increased slightly if the -v option is added to the command line. When mail1q is run in verbose mode, it adds a Priority field between the Size and Q-Time fields. The Priority field lists the queue priority of the message calculated by Sendmail. The numeric priority value may be ended with an optional +. The + indicates that a warning message about the delivery failure has been sent to the originator of the message. Listing 10.6 shows verbose mail1q output.