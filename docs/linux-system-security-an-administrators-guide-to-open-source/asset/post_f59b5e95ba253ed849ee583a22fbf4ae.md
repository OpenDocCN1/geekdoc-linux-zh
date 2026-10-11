
## Chapter 6 One-Time Passwords 117

Just Once,  
Only Once!

- The Purpose of One-Time Passwords ....... 118
- S/Key 118
- S/Key OTP Overview 119
- S/Key Version 1.1b 121
- S/Key Version 2.2 132
- OPIE 132
  - Obtaining and Installing OPIE 133
  - Implementing and Using OPIE 139
- OPIE and PAM 143
  - Obtaining and Installing pam_opie 143
  - Obtaining and Installing pam_if 144
  - Implementing pam_opie and pam_if 144
- Which OTP System Should I Use? 147
  - Advantages and Disadvantages of S/Key 147
  - Advantages and Disadvantages of OPIE 147
- S/Key and OPIE Vulnerabilities 147
- Summary 148
- For Further Reading 148
- Programming 148
- E-Mail Lists 148

## Chapter 7 System Accounting 149

Bean  
Counting

- General System Accounting 149
- Connection Accounting 150
- The last Command 151
- The who Command 152
- One Other Command 153
- Process Accounting 153
  - The sa Command 154
  - The lastcomm Command 155
- Accounting Files 156
- Summary 157
- For Further Reading 157
  - Books 157
  - On-Line Documentation 157

## Chapter 8 System Logging 159

And You  
Thought  
Wiretapping  
Was for the  
Feds!

- The syslog System Logging Utility 159
- Overview 160
- The /etc/syslog.conf File 160
- Invoking the syslogd Daemon 164
- Configuring /etc/syslog.conf 164
- The klogd Daemon 170
- Other Logs 170
- Alternatives to syslog 171
- The auditd Utility 171
- Summary 171
- For Further Reading 172
- General System Logging 172
- Intrusion Detection 172

## Chapter 9
Want To Be root?

- Superuser Do (sudo) 173
- What Is sudo? 173
- Obtaining and Implementing sudo 174
- Features of Version 1.5.9p4 174
- Implementing Version 1.5.9p4 175
- Using sudo 178
- The Functionality of sudo 178
- The /etc/sudoers File 178
- General Syntax of /etc/sudoers 181
- The visudo Command 184
- Options to the sudo Command 184
- A More Sophisticated Example 185
- Setting Up sudo Logging 188
- Reading sudo Logs 189
- PAM and sudo 189
- Disabling root Access 190
- Vulnerabilities of sudo 191
- Summary 191
- For Further Reading 191
  - Reference Books 191
  - E-Mail Lists 192
  - Web Sites 192
  - On-Line Documentation 192
  - Kerberos Resources 192
  - FWTK Resources 192

## Chapter 10
Which Doors Are Open?

- Securing Network Services: TCP_wrappers, portmap, and xinetd 193
- TCP_Wrappers 194
- Building TCP_Wrappers 196
- Access Control with TCP_Wrappers 202
- TCP_Wrappers Utility Programs 216
- TCP_Wrappers Vulnerabilities 218
- The Portmapper 218
- Building the Portmapper 219
- Implementing Portmapper Access Control 223
- The portmap Log Entries ... 224
- Gracefully Terminating and Recovering the Portmapper ... 224
- Portmapper Vulnerabilities ... 226
- Unwrapped Services ... 226
- Replacing inetd with xinetd ... 226
- Advantages of xinetd ... 227
- Disadvantages of xinetd ... 228
- Obtaining xinetd ... 228
- Building xinetd ... 229
- The xinetd Configuration File ... 232
- The xinetd Daemon ... 250
- Which One Should I Use? ... 252
- Summary ... 253
- For Further Reading ... 253
  - Resources for TCP_Wrappers ... 253
  - Resources for the Portmapper ... 254
  - Resources for xinetd ... 254
  - Internet Services Resources ... 255

## Chapter 11

- The Secure Shell ... 257
- Overview of SSH ... 257
- Host-Based Authentication Using RSA ... 257
- Authenticating the User ... 259
- Available Versions of SSH ... 263
- Obtaining and Installing SSH ... 264
- Compiling SSH ... 265
- Configuring the Secure Shell ... 267
- Configuring the Server Side ... 269
- Configuring the Client Side ... 275
- Using SSH ... 282
- Configuring SSH Authentication Behavior ... 282
- sshd Missing in Action ... 282
- Authentication Flow of Events ... 283
- Nonpassword Authentication ... 289
- Password-Based Authentication ... 304
- Exploring ssh Functionality ... 304
- ssh Examples ... 304
- scp Examples ... 306
- Port Forwarding and Application Proxying ... 307
- Secure Shell Alternatives ... 310
- Summary ... 312
- For Further Reading ... 312

![](img/7933c44717ab0711177ea7153f959fc5_15_0.png)

## Chapter 12

Crack......................................................................................................313

- Obtaining Crack................................................................................314
- Major Components of Crack..................................................................314
- Crack Overview.....................................................................................315
- Building Crack.....................................................................................318
- Modifying Crack for Linux........................................................................318
- Modifying Crack for MD5........................................................................319
- Modifying Crack for Bigcrypt....................................................................319
- Preparing Crack for crypt(3)......................................................................320
- Compiling and Linking Crack....................................................................320
- Compiling Crack Itself................................................................................320
- Crack Dictionaries...................................................................................321
- Obtaining Other Crack Dictionaries................................................................323
- Using Crack..........................................................................................323
- Running Crack......................................................................................328
- Running Crack over the Network...................................................................330
- Crack7...................................................................................................330
- Crack Rules...........................................................................................330
- What Do We Do about Cracked Passwords?..............................................336
- The White Hat Use of Crack.......................................................................337
- Effectively Using Crack..........................................................................338
- Summary..............................................................................................339
- For Further Reading..............................................................................339

## Chapter 13

Auditing Your System with tiger.....................................................................341

- Overview of tiger....................................................................................341
- Obtaining tiger......................................................................................342
- Major Components of tiger.........................................................................342
- Overview of tiger Configuration...................................................................347
- Overview of Run-Time Operation...................................................................360
- tiger Scripts...........................................................................................361
- Installing tiger to Run through cron............................................................368
- Which Scripts Should I Run?.......................................................................370
- cronre for a Development Machine................................................................372
- Running Crack from tiger..........................................................................373
- Deciphering tiger Output...........................................................................373
- Troubleshooting tiger...............................................................................375
- Modifying tiger......................................................................................376
- Modifying Scripts....................................................................................376
- Adding New Checks..................................................................................377
- Signatures.............................................................................................379
- Recommendations...................................................................................379
- Summary..............................................................................................379

![](img/7933c44717ab0711177ea7153f959fc5_16_0.png)

![](img/7933c44717ab0711177ea7153f959fc5_16_1.png)
