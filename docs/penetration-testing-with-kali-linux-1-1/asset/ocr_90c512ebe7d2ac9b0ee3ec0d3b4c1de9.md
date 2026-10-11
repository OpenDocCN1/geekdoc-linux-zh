![](bbox=[0.25, 0.14, 0.75, 0.47])

*Figure 309: Diagram of NTLM authentication in Active Directory*

In the first authentication step, the computer calculates a cryptographic hash, called the *NTLM hash*, from the user’s password. Next, the client computer sends the user name to the server, which returns a random value called the *nonce or challenge*. The client then encrypts the nonce using the NTLM hash, now known as a *response*, and sends it to the server.

The server forwards the response along with the username and the nonce to the domain controller. The validation is then performed by the domain controller, since it already knows the NTLM hash of all users. The domain controller encrypts the challenge itself with the NTLM hash of the supplied username and compares it to the response it received from the server. If the two are equal, the authentication request is successful.

As with any other hash, NTLM cannot be reversed. However, it is considered a “fast-hashing” cryptographic algorithm since short passwords can be cracked in a span of days with even modest equipment⁴43.

> *By using cracking software like Hashcat with top-of-the-line graphic processors, it is possible to test over 600 billion NTLM hashes every second. This means that*

⁴43 (Jeremi M Gosney, 2017), https://gist.github.com/epix0ep/ace60d99981be09544fdd35005051505