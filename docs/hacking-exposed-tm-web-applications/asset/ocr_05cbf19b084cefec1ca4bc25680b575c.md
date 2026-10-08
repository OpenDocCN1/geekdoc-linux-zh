# Chapter 12: Web Client Hacking

# 293

# Cookie Manipulation with Achilles

| Popularity: | 7 |
| Simplicity: | 5 |
| Impact: | 2 |
| Risk Rating: | 5 |

The easiest way to hijack cookies is to sniff them off the network and then replay them to the server, spoofing anyone's identity. Of course, obtaining the necessary network access to permit sniffing cookies is a challenge, so attackers will likely adopt more clever mechanisms.

> Don't discount cookie sniffing—on large corporate networks, Web browsing traffic passes many other potential eavesdropping points on its way to the Internet!

One of our favorite tools for implementing more targeted cookie attacks is Achilles, which we've discussed often in this book. To review, Achilles is a proxy server that intercepts web communications and allows editing of the traffic. You run Achilles on your machine and set your web browser to use it as a proxy. Voila—all communications between you and the Web pass through Achilles, set Internet Explorer to use the default local proxy port on your machine, select Tools | Options, click the LAN settings, and then select localhost and 5000 in the Proxy box as shown in Figure 12-6.

Once this is done, Achilles as shown in Figure 12-7 and start the proxy by clicking the button with the "play" icon. Now browse to any site in your browser and then examine Achilles interface. You can see the data sent by the browser in Achilles data window, down as shown in Figure 12-7. By clicking the Send button, the request will be sent to the server. You can then repeat this process with the response sent by the server, the next request from the web browser, and so on.

As you see in Figure 12-7, one of the values stored in the cookie is the IDUSER token. This value is stored in cleartext in the cookie, and is easily manipulated using Achilles. Before this request is sent to the server, we can simply edit the ID=USER value so it reads ID=ADMIN (or something similar—it may take a few guesses to get it right). When we click Send in Achilles, an initial request has now the context of ID=ADMIN (whatever it may be, but we're betting it means something for this app!)

The preceding example used a relatively straightforward way of user ID values, we've seen numerous variations on this. When auditing a Web app for related issues, some key flags to look for include (for example, "USER=JDOE\), anything with a substring of ID (for example, "ID=JDOE" or "SESSIONID=BLAHBLAH"), admin (for example, "ADMIN=TRUE"), session (for example, "SESSION=BLAHLAH"), cart (for example, "CART=FULL"), and expressions as TRUE, FALSE, ACTIVE, and

![](bbox=[0.075, 0.103, 0.128, 0.143])