
# Table B.2 Debugging Level Settings (continued)

| Setting | Information Displayed |
| --- | --- |
| 5.6 | A message when an event is triggered. |
| 6.1 | The error mode used when a message fails to be delivered. |
| 6.5 | The current error state. |
| 6.20 | The sender address of returned mail. |
| 7.1 | The unique identifier used for the queue files. |
| 7.2 | The complete queue filename. |
| 7.9 | The file descriptor for the queue file. |
| 7.20 | The name of each queue file as it is being processed. |
| 8.1 | An error message if an MX lookup fails. |
| 8.2 | A trace of the hostname lookup process. |
| 8.3 | A message indicating the local system is the preferred MX server. |
| 8.5 | Each hostname being sent to DNS. |
| 8.7 | A yes or no indicating if the hostname lookup was successful. |
| 8.8 | Resolver debug output for failed MX lookups. |
| 8.20 | An error message when the resolver library fails. |
| 9.1 | Responses to identd queries. |
| 9.3 | The identd response in its raw format. |
| 9.10 | The identd query being sent. |
| 10.1 | The delivery triple for the controlling recipient. |
| 10.2 | The address of the controlling user for this recipient. |
| 10.5 | The MeToo address if MeToo is not true. |
| 10.100 | A dump of all file descriptors before delivering the mail. |
| 11.1 | A trace of the mail delivery. |
| 11.2 | The real and effective user ID and group ID used for mail delivery. |
| 11.20 | The directories used by Sendmail during the mail delivery. |
| 12.1 | The recipient host address before being made RFC 822 compliant. |
| 13.1 | The delivery mode and recipient information for each piece of mail. |
| 13.5 | Recipient addresses to which mail should not be delivered. |
| 13.6 | A trace of the envelope processing. |
| 13.10 | The envelope identifier and flags. |
| 13.20 | The final delivery mode. |
| 13.21 | The final send queue. |
| 13.25 | A trace of the owner deliveries. |
| 13.29 | A status message after no recipients are left to process. |
| 13.30 | Messages relating to a scan of the send queue. |
| 14.2 | Each recipient header line that may need commas added. |
| 15.1 | Information about connecting a listener to port 25. |
| 15.2 | A message about forking a child to handle incoming mail. |
| 15.101 | Output from TCP kernel debugging for incoming connections. |
| 16.1 | Information about outbound TCP connections. |
| 16.101 | Output from TCP kernel debugging for outgoing connections. |
| 17.1 | A colon-separated list of MX records returned by DNS. |
| 17.9 | The hash used to randomize MX records that have equal preference. |
| 18.1 | All SMTP responses sent from this server. |
| 18.2 | The preparation of the MAIL From: header. |
| 18.100 | This halts Sendmail on an SMTP read error. |
| 19.1 | Optional ESMTP MAIL From: and RCPT To: parameters. |
| 20.1 | The delivery address before processing rulesets 3 and 0. |
| 21.1 | A trace of address rewriting similar to -bt output. |
| 21.2 | The current value of runtime variables. |
| 21.3 | The output of each ruleset that is called. |
| 21.4 | The rewritten address produced by each rule. |
| 21.10 | A message when the address does not match the rule pattern. |
| 21.12 | A message when the address matches the rule pattern. |
| 21.15 | The replacements made by indefinite tokens. |
| 21.35 | Every token match in each rule. |
| 21.36 | Every class variable match in each rule. |
| 22.1 | A trace of the tokenizing process. |
| 22.11 | The address before it was tokenized. |
| 22.12 | The address after it was tokenized. |
| 22.36 | Each token taken from the address as it was tokenized. |
| 22.101 | A character-by-character trace of tokenizing the address. |
| 24.4 | A message showing internal address-processing flags. |
| 24.5 | A trace of the flags and tokens used to build an address. |
| 24.6 | The result of building the address from tokens. |
| 25.1 | Each recipient as it is added to the send list. |
| 26.1 | Each recipient address as it is added to the send queue. |
| 26.8 | Addresses being tested for endless loops. |
| 26.10 | The contents of the entire send queue after loop checking. |
| 27.1 | A trace of the aliasing process. |
| 27.2 | The name of each file involved in aliasing. |
| 27.3 | The pathname of each forwarding directory. |
| 27.4 | The name of any file not owned by the user or root. |
| 27.5 | A detailed dump of each address processed by aliasing. |
| 27.8 | The value set for the aliases database. |
| 27.9 | The changes to user ID and group ID that occur during aliasing. |
| 27.14 | The controlling user when a change in user ID or group ID occurred. |
| 27.20 | The alias query created by Sendmail. |
| 28.1 | A trace of user database lookups. |
| 28.2 | A message when a user database lookup fails. |
| 28.4 | A status message each time a database is opened. |
| 28.8 | A status message when hesid is used to process logins. |
| 28.16 | Any MX records for the host to which mail is being forwarded. |
| 28.20 | A message each time the user database lookup is called. |
| 28.8 | The query sent to the user database. |
| 29.1 | The address sent to ruleset 5. |
| 29.4 | A trace of any attempt to match the address to cache data. |
| 29.5 | The address being tested for ruleset 5 processing. |
| 29.7 | A message indicating that matching failed. |
| 30.1 | A message indicating the end of the header section was found. |
| 30.2 | Messages indicating that the Unix header has been processed. |
| 30.3 | The header added to a mail missing a recipient header. |
| 30.35 | The machine state in inbound mail is collected. |
| 30.94 | The machine state for each individual character in inbound mail. |
| 31.2 | A message when the From: and Received From: headers are checked. |
| 31.6 | A status message as each header is processed. |
| 32.1 | The headers taken from inbound mail. |
| 32.2 | The processed header if the outdated -ba switch was set. |
| 33.1 | The full address line and the cleaned-up address. |
| 34.1 | A message when the routine that adds headers is entered. |
| 34.11 | A trace of the process of inserting headers. |
| 35.9 | The name and value of each variable as it is defined. |
| 35.14 | The internal identifier used for each variable. |
| 35.24 | Each variable before and after it has been expanded. |
| 36.5 | A trace of the symbol table processing. |
| 36.9 | The hash value used for each symbol table entry. |
| 36.90 | The name and type of each symbol from the table as it is applied. |
| 37.1 | The name and value of each option as it is set. |
| 37.8 | The class name and value as each value is added to the class. |
| 38.2 | A message as each database is initialized and opened. |
| 38.3 | A message for each of three passes used to open each database. |
| 38.4 | The result of each map open. |
| 38.9 | A message as each database is closed. |
| 38.10 | A trace of the search for the end of the alias database when NIS is used. |
| 38.12 | A trace of values being written to maps that allow updates. |
| 38.19 | A status message when the nswitch.conf file is used. |
| 38.20 | A detailed trace of database lookups. |
| 38.44 | The results of NIS hostname lookups. |
| 39.1 | The results of database lookups after applying replacement values. |
| 40.1 | A trace of storing mail in and retrieving mail from the queue. |
| 40.3 | The envelope flags from the queue entry. |
| 40.4 | Each line from the queue file as it is read. |
| 40.8 | An error message if Sendmail was unable to process a queue file. |
| 40.9 | The queue file and lock file descriptors. |
| 40.32 | A list of the send queue recipients. |
| 41.1 | The queue as it is ordered for processing. |
