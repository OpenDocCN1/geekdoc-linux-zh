+   before I start sending, I have to tell you that I'm going to send a book, otherwise you won't know what to do with a card (packet) when it arrives – that it is part of a book. Also I might be sending you several different books or magazine articles in several different streams, or you might already be sending another book to me. We avoid mixing up the different streams of cards (TCP connections) by marking each card with a unique reference for this stream. (With TCP, the combination (N$_1$, P$_1$, N$_2$, P$_2$) of source and destination IP and port numbers is the unique reference – see Module 10.4.)

+   I put sequence numbers on the cards (packets). If they arrive out of order you rearrange them into the correct order

+   as you receive packets you occasionally send me an acknowledgment card (packet) telling me the last one in sequence that you received. I can see if some have got lost, and can re-send those after the last one I know you received. (You could send an acknowledgment card for every card I sent you, but that would slow things down a lot. When we set up the connection in the first place, you tell me how many cards I can send you before I should expect an acknowledgment)

+   your acknowledgment cards (packets) can get lost too, so if I have sent a lot of cards (packets) and haven't had any acknowledgment for a long time, I re-send the cards (packets) after the last sequence number that you did acknowledge

+   neither of us has to understand the content of what I'm sending, only the system of sequence numbers and acknowledgments. Even if the information we're sending is in ancient Greek, the system works and we can both be sure that you got everything I sent, and in the correct order. (TCP just delivers “data” to the application without attaching any particular meaning to it. It's the application in the layer above that interprets the data – it adds the semantics. For example, the telnet application (Module 10.6) treats the data as characters to be printed on screen or to be sent to the shell, etc. whereas an FTP server application which receives “GET cat.gif” realizes this is a request to download that file to the client

+   only you and I pay any attention to the sequence numbers and acknowledgment cards (packets). To everyone in the middle – messenger boy, mail clerk, etc. (routers on the Internet) – a card (packet) is just something to be forwarded to its destination. (TCP is used only on the source and destination machines. The IP layer alone is used on the intermediate routers.)

+   at the end, I tell you when I've finished sending so you know that you've received everything and that there's no more to come.

The end result is that TCP is reliable, in the strict networking sense: you receive exactly what I send, and in the correct order, without duplicates.

This analogy isn't rigorous – it's only to give you a gut feel for how TCP works. TCP has lots of subtleties that we haven't included. In particular TCP supports two-way traffic over a single connection, and the acknowledgment packets can also contain data, to make the whole process as efficient as possible. (See the Notes for further information.)