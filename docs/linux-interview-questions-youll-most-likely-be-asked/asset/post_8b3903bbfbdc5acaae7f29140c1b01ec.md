
158: What is the command to kill a process by the PID of the process?

Answer: kill

159: What does the "-9" flag to the above command do?

Answer: Forces the process to terminate, often resulting in the loss of data.

160: What does the "-HUP" flag to the above command do?

Answer: Stops, and then restarts the process.

161: What command will allow you to view the running processes on the server, sorted by CPU utilization, in real time?

Answer: top

162: What key, when pressed while running the above command, will allow you to terminate a process?

Answer: K

163: What command will allow you to adjust the priority of a process (in terms of system resources)?

Answer: nice

164: What is the exact syntax to launch a script named 'script.sh' (using the above utility), with the lowest system priority?

Answer: nice -n 20 script.sh

165: What is the exact syntax to launch a script named 'script.sh' (using the above utility), with the highest system priority?

Answer: nice -n -20 script.sh

166: What number corresponds to the default system priority?

Answer: 0

167: What command will allow you to adjust the priority of an already running process?

Answer: renice

## Networking

168: What TCP port does HTTP run on?

Answer: 80

169: What TCP port does SSH run on?

Answer: 22

170: What TCP port does SMTP run on?

Answer: 25

171: What TCP port does SSL run on?

Answer: 443

172: What is the default port for the submission service?

Answer: 587

173: What TCP port does POP3 run on?

Answer: 113

174: What TCP port does FTP run on?

Answer: 21

175: What TCP port does Squid, or most other HTTP proxies, run on?

Answer: 8080

176: What TCP port does CIFS/SMB (also called NETBIOS) run on?

Answer: 139

177: What file contains the default applications, and port numbers associated with them?

Answer: /etc/services

178: What TCP port does DNS run on?

Answer: 53

179: What TCP port does MySQL run on?

Answer: 3306

180: What command is used to find the packet route between the server you are on, and a host located on another network, called example.com?

Answer: traceroute example.com

181: What command can be used to send a test packet to ensure that a host is responding to ICMP packets?

Answer: ping

182: What is the highest priority a mail server can have, on a DNS MX record?

Answer: 0

183: What is the name for a DNS record that points to an IP address?

Answer: A Record

184: What is the name for a DNS record that points to another DNS record?

Answer: CNAME Record

185: What is the 'TTL' setting on a DNS record for?

Answer: “Time to Live”, or the time that a record is valid, in seconds. After the TTL period, the record expires, and DNS servers should no longer cache the response.

186: What is a SPF record used for?

Answer: A domain-based anti-spam protection. It specifies which hosts are allowed to send mail for a domain.

187: What is the difference between DKIM, and SPF?

Answer: DKIM digitally signs emails (to confirm that the mail message came from a mail server that is the authoritative mail server for that domain), SPF specifies which hosts are allowed to send mail on behalf of that domain. DKIM requires a software implementation on the sending server, SPF is purely a DNS record, requiring no further software installation.

## Postfix

188: What configuration file controls the majority of Postfix’s configuration?

Answer: /etc/postfix/main.cf

189: What configuration file controls what TCP ports Postfix listens on, as well as the different options enabled on each Postfix instance?

Answer: /etc/postfix/master.cf

190: What file contains all mailbox aliases on the Linux server?

Answer: /etc/aliases

191: What command should be ran after updating the above file?

Answer: newaliases

192: What does the option "mynetworks" control?

Answer: Which networks are allowed to relay mail through the Postfix server.

193: What is the option that controls which domains Postfix will accept mail for (for multiple domains)?

Answer: mydestination

194: What is the default mail delivery location?

Answer: /var/mail/username, or /var/spool/mail/username

195: What is the default mail log location?

Answer: /var/log/mail.log

196: What is the default mail error log location?

Answer: /var/log/mail.err

197: What is the command to restart Postfix?

Answer: /etc/init.d/postfix restart

198: What authentication method does Postfix support, for authenticating SMTP users securely (via local UNIX accounts, or even a MySQL database)?

Answer: SASL

199: What command can you use to manually start a SMTP conversation with a mail server running on example.com, in order to troubleshoot mail delivery issues?

Answer: telnet example.com 25

200: What is the first command that is ran at the beginning of every SMTP connection (per RFC 2821)?

Answer: EHLO

## HR Questions

Review these typical interview questions and think about how you would answer them. Read the answers listed; you will also find some strategy suggestions with it.

1: How do you make decisions?

Answer: This is a great opportunity for you to wow your interviewer with your decisiveness, confidence, and organizational skills.

Make sure that you outline a process for decision-making, and that you stress the importance of weighing your options, as well as in trusting intuition. If you answer this question skillfully and with ease, your interviewer will trust in your capability as a worker.

2: What are the most difficult decisions for you to make?

Answer: Explain your relationship to decision-making, and a general synopsis of the process you take in making choices. If there is a particular type of decision that you often struggle with, such as those that involve other people, make sure to explain why that type of decision is tough for you, and how you are currently engaged in improving your skills.

3: When making a tough decision, how do you gather information?

Answer: If you’re making a tough choice, it’s best to gather information from as many sources as possible. Lead the interviewer through your process of taking information from people in different areas, starting first with advice from experts in your field, feedback from coworkers or other clients, and by looking analytically at your own past experiences.

4: Tell me about a decision you made that did not turn out well.

Answer: Honesty and transparency are great values that your interviewer will appreciate – outline the choice you made, why you made it, the results of your poor decision – and finally (and most importantly!) what you learned from the decision.

Give the interviewer reason to trust that you wouldn’t make a decision like that again in the future.

5: Are you able to make decisions quickly?

Answer: You may be able to make decisions quickly, but be sure to communicate your skill in making sound, thorough decisions as well. Discuss the importance of making a decision quickly, and how you do so, as well as the necessity for each decision to first be well-informed.

6: Why would your skills be a good match with $X$ objective of our company?

Answer: If you’ve researched the company before the interview, answering this question should be no problem. Determine several of the company’s main objectives, and explain how specific skills that you have are conducive to them. Also, think about ways that your experience and skills can translate to helping the company expand upon these objectives, and to reach further goals. If your old company had a similar objective, give a specific example of how you helped the company to meet it.

7: What do you think this job entails?

Answer: Make sure you've researched the position well before heading into the interview. Read any and all job descriptions you can find (at best, directly from the employer's website or job posting), and make note of key duties, responsibilities, and experience required. Few things are less impressive to an interviewer than a candidate who has no idea what sort of job they're actually being interviewed for.

8: Is there anything else about the job or company you'd like to know?

Answer: If you have learned about the company beforehand, this is a great opportunity to show that you put in the effort to study before the interview. Ask questions about the company's
