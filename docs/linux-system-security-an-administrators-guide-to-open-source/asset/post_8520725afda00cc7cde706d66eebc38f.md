
## PAM
continued

- and login, 93
- login time and location restrictions, 95–98
- and MD5, 88, 91
- module types, 84
- and OPIE, 143
- overview, 82–86
- pam_access, 104, 110, 304
- pam_cracklib, 89–93, 338
- pam_deny, 108
- pam_if, 144–146, 189
- pam_lastlog, 106
- pam_limits, 98
- pam_listfile, 100–102
- pam_nologin, 94, 144
- pam_opie, 143–145, 189
- pam_persmit, 109, 128
- pam_pwdb, 87–89, 90–93, 145, 189
- pam_rhosts_auth, 107
- pam_rootok, 100
- pam_security, 93
- pam_time, 95–98
- pam_warn, 108
- pam_wheel, 103, 173, 189
- PAM-aware applications, 113
- and passwords, 86–93
- and SSH, 304
- standard arguments, 85
- and su, 103
- and sudo, 177, 189
- and Sun Microsystems, Inc., 81
- and TCFS, 425–426
- wheel group, 103

## password

- aging, 61–64
- cracking, 4
- database library (pwdb), 86, 550
- file, 1, 60
- hashing, 45
- Linux, 58–59
- one-time (OTP), 44, 59, 117–148, 519, 534, 550
- and PAM, 108, 143–145

## path
shell variable, 4

## PGP
45–47, 534, 550

- and Crack, 314
- and GNPUP, 46
- and OpenPGP, 46
- GPGPASSFD, 400, 401
- and public keys, 46
- and RPM, 27
- and S/Key, 119
- and tiger, 342
- and Tripwire, 383, 397–401

## pluggable authentication modules
See PAM

## POP
22

## port numbers
33

## portmap
218–226, 521, 550

- /etc/hosts.allow, 223
- /etc/hosts.deny, 223
- access control, 222
- compiling and installing, 219–222
- obtaining, 219
- pmap_dump, 224
- pmap_set, 224
- vulnerabilities, 226

## portmapper
See portmap

## PPP
470, 481, 487, 550

## Pretty Good Privacy
See PGP

## process accounting
See system accounting

## pwdb
See password

## R

- rdist, 182, 301
- Red Hat, 534, 541
- Red Hat Package Manager. See RPM
- reliability, 13
- remote procedure calls (RPC), 36
- request for comments (RFC), 40, 551
- RFC 1918 (reserved internal addresses), 459
- risk analysis, 12, 14

## root

- account, 66, 518–519
- disabling direct access to, 190–191
- and groups, 70
- restricting access to, 102, 103, 190, 298–299

## RPM
26–28, 523, 533, 541

- and MD5, 26, 27
- and PGP, 27

## rsysd
182, 301

## run levels
24–26

## S

## S.u.S.E.
536, 542

## S/Key
117, 118–132, 519, 536

- /etc/skeykeys, 120, 124, 125, 130, 133
- key, 120, 123, 124, 126, 127, 129–130, 133
- keyaudit, 131, 133
- keyinfo, 124, 125, 133
- keyinit, 120, 123–126, 128–133
- keyssh, 123–129, 131, 133
- and make, 122–124
- overview, 119
- and sudo, 175
- version 1.1b, 121–132
- version 2.2, 132
- vulnerabilities, 147

## sa
See system accounting

## safe environment
48, 100, 114

## SAGE
535

## Samba
37, 551

## SANS
49, 535, 541

## secure Linux projects
535

## Secure Shell
See SSH

## Secure Socket Layer (SSL)
311

## SSLkey
311, 546

## secure_delete
432

## security

- archives, 47
- and ethics, 18
- implementing and managing, 516–527
- mailing lists, 538–542
- and people, 15
- rules of thumb, 15–18
- server, 392

## Security Policy
3, 6, 14–17, 515, 516, 519, 520, 521, 522, 523, 524, 525, 526

- and Crack, 338
- defined, 12

## sendmail
8, 22, 26, 33, 536

## SGID
5, 74

## SHADOW
545

## shadow file
1, 61–64, 551

## shell
restricted, 59, 64

## single-user mode
24

## Slackware
536

## slesshost
536

## sniffit
38

## social engineering
6

## SOCKS
436, 486, 545

## software testing
48

## source code auditing
48

## spoofing
5

## See also
Internet Protocol and DNS

## SSH
257–312, 435, 518, 520, 521, 526, 536, 541, 551

- authentication behavior, 282–304
  - flowchart, 283
- Blowfish, 258, 276
- compiling and installing, 265
- configuration files defined, 267
- configuring, 267–281
  - client-side (ssh), 275–281
  - server-side (sshd), 269–275
- DES, 276
- description of keys, 262
- encrypting X sessions, 287, 293, 295, 299–303, 305
- and /etc/hosts.allow, 266, 270, 283, 310
- and /etc/hosts.deny, 266, 270, 283, 303, 310
- Host-Based Authentication
  - concepts, 257–259
  - configuration, 285–288
- IDEA, 258, 276
- and ipchacha, 453, 464, 470, 480–481
- Nonpassword Authentication, 289–303
- obtaining, 264
- overview, 257–265
- and PAM, 304
- Password Authentication, 263, 303
- port forwarding and proxying, 307–310
- Rhosts and RSA Authentication
  - concepts, 260
  - configuration, 289–293
- Rhosts Authentication
  - concepts, 260
  - configuration, 289
- RSA Authentication
  - concepts, 260–262
  - configuration, 293–303
- running sshd, 282
- scp examples, 306
- ssh-add, 295, 301, 302, 312
- ssh-agent, 262, 278, 295, 300, 301, 302, 312
  - and ssh not running, 282
  - and TCP_wrappers, 283
- start-up scripts, 24–26

## sudo
173–192, 520–521, 542, 552

- /etc/sudoers, 178–183, 191
- and configure, 175–177
- and DNS, 176
- and FWTK, 175
- installing, 175–177
- insults, 176, 181
- and logging, 175, 188–189
- and make, 177
- obtaining, 174
- and OPIE, 175
- and PAM, 175, 177, 189
- and S/Key, 175
- and umask, 176
- visudo, 184

## SUID
4, 74

## swatch
160, 491, 498–507, 525

- and CPAN, 500
- configuring, 503
- installing, 500–503
- obtaining, 499

## syslog
159–169, 173, 491, 492, 496, 552

- and ipchains, 450
- and sudo, 175
- and TCP_wrappers, 196

## system accounting
149–156

- /var/log/pacct, 153
- ac, 151
- accton, 154
- connection accounting, 150–153
- dump-acct, 154
- dump-utmp, 150
- last, 151
- lastcomm, 155
- lastlog, 153
- and PAM, 106
- process accounting, 153–156
- sa, 154
- tlog, 150
- who, 152
- wtmp, 150

## system logging
159–170

## T

## TCFS
415–433, 435, 542, 552

- client-side configuration, 417–424
- commands, 425
- compared to CFS, 431
- components of the distribution, 418
- DES, 423
- extended attributes, 427
- installing, 417–424
- key management, 429
- and NFS, 405, 416, 418, 426, 431
- obtaining, 416
- overview, 416
- and PAM, 425
- rebuilding the kernel, 420–424
- server-side configuration, 424
- using, 425–430
- vulnerabilities, 430

## TCP_wrappers
194–218, 435, 521, 552

- /etc/hosts.allow, 202–216
  - access control, 202–205
  - using one file, 213
- banners, 206–210
- compiling and installing, 196–201
- and /etc/inetd.conf, 194–196
- and inetd, 196
- obtaining, 194
- spam, 210–211
- and SSH, 283
- and syslogd, 196
- tcpd, 194, 196, 202–207, 212, 213, 218, 227, 249, 253, 254
- tcpdchk, 199, 216, 254
- tcpdmatch, 199, 216, 217, 254
- try-from, 216, 217
- twist, 211–213
- and xinetd, 249
- vulnerabilities, 218

## tcpd
See TCP_wrappers, 196

## tcpsvd
38

## threat assessment
74

## tiger
44, 49, 73, 74, 341–379, 525, 542

- binaries, 347
- check_accounts, 361
- check_aliases, 361
- check_anonftp, 362
- check_cron, 362
- check_embedded, 363
- check_exports, 363
- check_group, 364
- check_inetd, 364
- check_known, 364
- check_netrc, 364
- check_nisplus, 364
- check_passwd, 364
- check_path, 365
- check_perms, 365
- check_printcap, 365
- check_rhosts, 365
- check_sendmail, 365
- check_signatures, 366
- check_symblink, 368
- check_system, 366
- configuration, 347–360
  - configuration files, 347–348
- and Crack, 373
- crack_run, 366
- and cron, 368–372
- deciphering output, 373–375
- directory tree, 342
- documentation, 347
- find_files, 367
- and MD5, 347, 378
- modifying, 375–378
- obtaining, 342
- overview, 341
- PGP, 342
- run-time operation, 360–368
- scripts, 344–347, 361–368, 370–371
- and signatures, 377
- site file, 349–350
- and Snefru, 347, 378
- tigercon, 359–371
- tigerco, 361–360
- tigero, 368
- troubleshooting, 375

## Transmission Control Protocol (TCP)
29, 32, 552

## Transparent Cryptographic File System
See TCFS

## TrinityOS
49, 484, 487, 536

## Tripwire
44, 49, 74, 381–403, 525, 552

- checkconfig, 385, 391
- compare mode, 399–402
- configuration file, 386–393
- database storage, 388
- and Haval, 387, 388, 402
- initialize mode, 396–399
- installation, 383–386
- Kim, Gene, 383
- and MD5, 384, 387, 388, 400, 402
- obtaining, 383
- options, 395
- overview, 382
- performance, 402
- and PGP, 383, 384, 397–401
- preprocessor syntax, 389–391
- selection masks, 387
- and SHA-1, 387, 388
- signer, 385
- and Snefru, 387, 388, 400, 402
- Spafford, Eugene H., 383, 384
- Tripwire Security Systems, Inc., 383
- tw_newnode.pl, 385
- twlb_check.pl, 383, 385, 403
- update mode, 402–403
- versions, 383
- zcryptoptl, 385

## Trojan horse
4, 67, 118, 365, 381

## U

## UID
See user

## underground
8, 9

## UPG
See groups

## USENET
537, 542

## user

- accounts, 57, 526
- identification number (UID), 64

## User Datagram Protocol (UDP)
32, 552

## utmp
See system accounting

## V

## Virtual Private Networks (VPN)
486

## visudo
See sudo

## vulnerabilities

- general, 1–9
- vulnerability assessment, 14

## W

## wheel group
103

## who
152

## wipe
432

## xmp
See system accounting

## X

## xinetd
226–253, 435, 525, 537, 553

- compiling and installing, 229–231
