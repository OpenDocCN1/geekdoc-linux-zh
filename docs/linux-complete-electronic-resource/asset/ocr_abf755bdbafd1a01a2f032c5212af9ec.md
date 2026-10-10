During this process, either capture (log to a file) the entire login process or carefully (*very carefully*) write down *exactly* what prompts the server gives you to let you know it is time to enter your user name and password (and any other commands needed to establish the PPP connection).

If your server uses PAP, you should not see a login prompt, but should instead see the text representation of the link control protocol (which looks like *garbage*) starting on your screen.

A few words of warning:

+   ▶ Some servers are quite intelligent: you can log in using text-based user name/passwords or using PAP. So if your ISP or corporate site uses PAP but you do not see the garbage start up immediately, this may not mean you have done something wrong.

+   ▶ Some servers require you to enter some text initially and *then* start a standard PAP sequence.

+   ▶ Some PPP servers are passive—that is, they simply sit there sending nothing until the client that is dialing in sends them a valid LCP packet. If the PPP server you are connecting to operates in passive mode, you will never see the garbage!

+   ▶ Some servers do not start PPP until you press *Enter*—so it is worth trying this if you correctly log in and do not see the garbage!

It is worth dialing in at least twice—some servers change their prompts (e.g., with the *time!*) every time you log in. The two critical prompts your Linux box needs to be able to identify every time you dial in are:

+   ▶ the prompt that requests you to enter your user name

+   ▶ the prompt that requests you to enter your password

If you have to issue a command to start PPP on the server, you will also need to find out the prompt the server gives you once you are logged in to tell you that you can now enter the command to start PPP.

If your server automatically starts PPP, once you have logged in, you will start to see garbage on your screen—this is the PPP server sending your machine information to start up and configure the PPP connection.

This should look something like this:

`^y|#.|1|]!) })8|}|$)*}!|& ) } } )}&& . . .|)|'(*|)^ . ^y)`

(and it just keeps on coming!)