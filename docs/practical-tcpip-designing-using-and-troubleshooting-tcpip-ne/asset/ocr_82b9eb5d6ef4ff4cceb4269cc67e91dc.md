Lines 78–79: HAL9000-NT still believes it's going to win the election and sends a few more confirming **Elections** If HAL9000-NT had not been the segMB already, i.e. if another machine had previously won an election, HAL9000-NT would now register itself as *domainname* **<1d>** to identify itself to other machines as the current segMB. However, as HAL9000-NT was already the segMB before this election started, it has no need to register itself as a *domainname* **<1d>** again.

Line 80: HAL9000-NT is now the browse master, and instructs AliceNT to become a backup browser. The protocol tree pane shows the detail of how HAL9000-NT tells AliceNT to do this.

Line 81: AliceNT configures herself as a backup browser, and sends an **Announcement Request** to check that there is a browse master. (You'd think she could remember this from Line 73, but it appears that the browser code internally is divided into separate chunks for the “client,” “backup browser,” etc. roles and there's no communication between them.)

Line 82: HAL9000-NT announces itself as the segment master browser

Line 98: AliceNT announces herself as a backup browser. HAL9000-NT hears this and adds AliceNT to its list of backup browsers.

The election is finished, HAL9000-NT is the segMB and AliceNT is acting as backup browser. The browse system is back to a steady state again, where all the browse servers know of one another and act accordingly, handling client requests, etc.

The browse system aims to have one backup browser for every 32 machines on the local segment. The segMB counts how many different machines have announced themselves, and for every 32, it instructs one to become a backup, as in line 80 above.

(A better name for an election packet would be a “bid” packet, because one machine doesn't elect another; it merely announces its own bid, and if nobody else bids higher, it knows it has been elected. This is like participating in an auction to buy something without an auctioneer. If I make a bid and nobody bids within a “reasonable amount of time” after me, I know I have purchased the item and go and pay the vendor.)

> Note: Netmon shows election packets slightly differently to **ethereal**. Netmon distinguishes between an **Election** (Force) packet to initiate an election, and an **Election** bid packet in response to the **Force**. **ethereal** just shows them all as **Elections** in the packet list pane (but of course you can see the full detail for each in the protocol tree pane).