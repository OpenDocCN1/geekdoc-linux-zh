The lpd.perms file consists of a set of rules that are sequentially evaluated until a match is found. The DEFAULT action rule should be the last rule and is normally one to accept any requests. In other words, any request that is not matched by the preceding rules is accepted. Normally, you would set up rules to reject certain requests, such as requests for specific hosts. Most requests would not match these rules and should fall through to the DEFAULT action, which would ACCEPT them.

SERVICE key values differ depending on the type of request submitted. These can range from a simple connection request by a remote server to a removal of a print job. The print clients such as lpr, lpq, lprm, and lpc make different kinds of service requests. lpq makes a request for queue information that has the key value Q for SERVICE. lprm issues a removal request indicated by a key value M.

# LPRng Print Clients

LPRng uses the same command line print clients as described for CUPS. These include the lpr, lpc, lpq, and lprm commands. Check the Man pages for each for detailed options. Certain features, like encryption, are available only with CUPS versions.