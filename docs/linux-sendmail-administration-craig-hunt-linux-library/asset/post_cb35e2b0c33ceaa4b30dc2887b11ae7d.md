
## e-mail addresses – FETCH command (IMAP4) 441

## E

### e-mail addresses
- basic types, 220
- formatting, 44–45
- parsing and rewriting, 204–205
- rewriting, 234
- rulesets to process, 221
- tokens in, 227

See also mail architecture
- insertion of header, 203–204
- maximum size, 337
- message headers, 13–15
- privacy, 342

- RFC 822 to define format, 131–212
- EHLO command (SMTP), 12, 20–21
- EightBitMode option in sendmail.cf, 424
- elm, filter tool, 315
- el symbol by pattern matching, 231
- embedded spaces in e-mail address, 195
- empty rulesets, 223
- encryption, 303–344

- End-of-line (E) field in mailer definition, 209, 210

- ENHANCEDSTATUSCODES, 21
- EnvFrom ruleset, 225
- EnvFromSMTP ruleset, 224
- environment variables in mailircfile, 315
- EnvTo. ruleset, 225, 228–229
- EnvToSMTP ruleset, 224
- error marker, 164
- $error mailer, 244, 313

### error messages
- defining in access database, 160, 310
- from mailertable, 167–168
- returning to sender, 164, 244–346
- sender name to generate, 183
- ErrorHeader option in sendmail.cf, 424
- ErrorMode option in sendmail.cf, 424
- smtp mailer, 119
  - definition, 206
  - mailertable feature for, 167
- /etc/mail directory, 75
- /etc/mail/relay-domains file, 145
- /etc/mail/trusted-users file, 144
- /etc/mail/userdb.database, 154–256, 256
- /etc/mail/proamird file, 315
- /etc/rdc.d/min directory, 51, 54
- ETRN keyword, 21

- EXAMINE command (IMAP4), 26
- exclamation point (!) for UUCP bang addressing, 188

- Expand command (SMTP), 5, 8
- expandable classes, 188

- EXPOSED_USER command (m4), 102, 104–105, 118, 255, 368
- EXPUNGE command (IMAP4), 27
- Extended SMTP, 20–22
  - mailer to support, 119

## F

- F (load) class, class variable from file, 190–191
- FallbackMXHost option in sendmail.cf, 425
- fax mailer, 391
- FAX_RELAY variable, 264, 386
- FEATURE command (m4), 92, 98, 362, 376–381
  - for database configuration, 142–143
  - format for, 96

- FETCH command (IMAP4), 27, 29

![](img/9639113aa446fb8976cb3d377f7aafdd_464_0.png)

## 442 field body in e-mail message – Hello command (SMTP)

- field body in e-mail message, 13
- field name in e-mail message, 13
- file security, 340–341
  - disabling, 199
- files, loading class variable from, 190–191
- final ruleset, 220, 222
- firewall, 332
  - commands, 108
  - contents, 97–98
  - DOMAIN command, 112–114
  - FEATURE command, 114–115
  - MAILER commands, 118–122
  - OSTYPE command (m4), 109–112
  - root account protection from masquerading, 117–118
- GENERIC_DOMAIN command (m4), 170, 362
- GENERIC_DOMAIN_FILE command (m4), 170, 256, 363
- generics_entire domain feature, 256, 377
- genericstable database, 169–171, 380
  - and masquerading, 256–258
- genericstable feature, 143, 377
- glint tool
  - flags
    - for address processing, 284–285
    - for mailers, 431–433
    - modifying, 104, 385
    - procmail recipe, 316
- Flags (F) field in mail definition, 208, 210
- flow control in rewrite rules, 234–237
- ForkEachJob option in sendmail.cf, 425
- Format of Headers section (sendmail.cf), 203–204
- formatting e-mail addresses, 44–45
- .forward file, 48, 153
  - location for, 200
  - path to locate, 113–114
  - security for, 340–341
- forwarding mail, 47
- alias for, 150, 152–153
  - vs. relaying, 48
- ForwardPath option in sendmail.cf, 425
- From command (SMTP), 5
- From: header, 14
- FTP, anonymous, to download RPM software, 64–65
- gnupm tool (GNOME), 69, 69
- Gnu Privacy Guard (GnuPG), 342
- GnuPGP (Gnu Privacy Guard), 342
- grep command, 124
- group ID for Sendmail, 125

## G

- gawk, 319
- gcc compiler, problems from, 74
- GDBM, incompatibility with Sendmail, 74
- generic-linux.cf file, 108
- generic-linux.mc file, 86–87, 108–122

## H

- H (define header) command, 203, 215
- H variable, 262
- HACK command (m4), 102, 103, 366, 366
- hacks, for temporary Sendmail configuration problems, 83–84
- hardware, security for, 322–323
- HdrFromL ruleset, 225
- HdrFromSMTP ruleset, 225
- headers
  - formatting, 46
  - maximum number of bytes for all, 114
- Hello command (SMTP), 5

## Help command (SMTP) - keyed file (K) 443

- Help command (SMTP), 5, 8
- HelpFile option in sendmail.cf, 425
- HoldExpensive option in sendmail.cf, 425
- hostnames
  - accepting mail for other, 115–116
  - adding to class, 148
  - blocking mail from fake, 306
  - hiding masquerading*
  - list to be masqueraded, 252
  - reasons for not advertising, 249
- hosts.allow file, 331
- hosts.deny file, 331
- HostsFile option in sendmail.cf, 425
- hoststat command, 273–276
- HostStatusDirectory option in sendmail.cf, 425
- hub

## I

- identd (auth server), 300
- identification daemon, 300–301
- ifdef command (m4), 110–111
- IgnoredDots option in sendmail.cf, 425
- image media type (MIME), 16
- IMAP (Internet Mail Protocol), 25–29
  - through stunnel, 329
- inbound mail
  - forwarding, 46
- header processing, 314
- include command (m4), 102, 103–104
- incoming spam, blocking, 305–314
- infinite tokens, 232–233, 240
- inetd configuration, removing daemons from, 327
- infinite loops
  - in mail routing, 262
  - in rewrite rules, 235, 236
- INPUT_MAIL_FILTER command (m4), 363, 389
- installing Sendmail, 61–71
  - cleanup after RPM, 69–71
  - configuration compatibility, 75–76
  - with dpkg, 61–62
- installing binaries, 73–74
- known problems, 74
- locating RPM software, 62–65
- anonymous FTP to download, 64–95
- using rpm.file, 63–64
- on web site, 62
- with RPM, 66–68
- tools for, 69
- Inter-Process Communication (IPC), 43
- Internet Mail Protocol (IMAP), 25–29
  - through stunnel, 329
- Internet Protocol suite, 3
  - ip address, 4
- in access database field, 158
- in e-mail address, 239
- IPC (Inter-Process Communication), 43

## J

- junk mail. See spam

## K

- (keyed file) command, 182, 191–197, 215
  - switches, 193–196
  - type argument, 192–193
- KDE desktop environment, tool, 68
- keyboard, security for, 323
- (keyed file (K)) command, 181–197
  - switches, 193–196
  - type argument, 192–193

## L

- kill command, 60–61
- mailer, 207
- localaddr ruleset, 220, 222
- Local_check_mail ruleset, 224, 313
- Local_check_rcpt ruleset, 224, 132, 349
- Local_check_relay ruleset, 223, 313
- LOCAL_CONFIG command (m4), 102, 104, 257, 363, 392
- LOCAL_DOMAIN command (m4), 148, 363, 390
- local_mtp feature, 377
- localaddr ruleset, 223
- LOCAL_NET_CONFIG command (m4), 261, 363, 395
- local_procmail feature, 111–112, 132, 377, 381
- LOCAL_RELAY define, 183, 386
- LOCAL_RULE_n command (m4), 102, 104, 363, 392
- LOCAL_RULESETS command (m4), 102, 104, 259, 363, 392
- LOCAL_trust_auth ruleset, 224, 249
- LOCAL_USER command (m4), 263, 363, 387
- locked room, for server, 323
- login access, limiting, 228–335
- LOGIN command (IMAP4), 26
- LogLevel option in sendmail.cf, 425
- LOGOUT command (IMAP4), 26
- host status, 275
- LookupAddress ruleset, 222
- LookUpDomain ruleset, 222
- loops in mail routing, 262
- in rewrite rules, 235, 236
- loose_relay_check feature, 377
- LSUB command (IMAP4), 27
- USER_RELAY macro, 264, 386
- LAST command (POP), 23
- LDAP mapping, 394
- LDAP map specification, 199
- LDAPDefault option in sendmail.cf, 424
- LDAPROUTE_DOMAIN command (m4), 363, 394
- LDAPROUTE_DOMAIN_FILE command (m4), 363, 394
- idap_routing feature, 377, 394
- limited_masquerade feature, 252, 377, 388
- LineLimit (L) field, manner definition, 209, 211
- Linux, default configuration for Sendmail, 40
- linuxconf
  - to create access database, 311, 312
  - to enable Sendmail, 57–58
- linux.m OSTYPE file, 109
- LIST command (IMAP4), 26
- LIST command (POP), 23, 25
- literals in pattern matching, 228
- load class (F) command, 190–191, 215
- loading class variable from file, 190–191
- load host alias, 47
- local-host-names file, 115, 116, 147–149
- Local Info section (sendmail.cf), 180–199
- class variable loading from file, 190–191
- def class (C) command, 186–190
- define macro (D), 182–186
- keyed field (K) command, 191–197
- version level (V) command, 197–199
- local mail, relay host to handle, 183

## M =M command - MAILER (smtp) command (m4) 445

- =M command, 291
- M (mailer) command, 205–211, 215
- samples, 210–211
- M variable, 183
- .m4 file extension, 84, 94
- m4 marco language, 82, 91–105
- command line, 99–100
- command order in configuration file, 97–98
- commands, 361–394
- DAEMON_OPTIONS command, 362, 393–394
- define command, 367–376. see also define command (m4)
- DOMAIN command, 386–390. see also DOMAIN command (m4)
- FEATURE command, 92, 96, 98, 142–143, 376–381
- LDAP map routing, 394
- local code, 392–393
- MAILER command, 89, 92, 95, 98, 118–122, 363–390
- OSTYPE command, 88, 89, 92, 96, 98, 109–112, 262, 364, 382
- g generic-linux.mc file, 98, 118–122
- MAILER-DAEMON alias, 152
- MAILER (local) command (m4), 95, 119
- miler (m4) command, 205–211, 215
- MAILER (procmail) command (m4), 131, 168
- mailer rulesets, 224–226
- MAILER (smtp) command (m4), 95, 119
- quick reference, 361–366
- configuration file, 94. See also .m4 file
- building simple, 99–102
- installing, 100–102
- putting in place, 101
- sample, 97–99
- output control, 92–94
- reasons to use, 216
- macro variables, expanding, 184

## Mail Abuse Prevention System (MAPS), 306–309

### mail architecture
- basics, 31–33
- components, 36–41
- common terminology, 38–39
- formal definitions, 36–41
- Mail Definitions section (sendmail.cf), 205–211
- mail delivery. See delivery triple
- Mail Exchange (MX) record, 33–34
- processing, 35–36
- Mail From: command (SMTP), 12
- mail hub, 38
- mail relay configuration to prevent spam, 301–305
- parameter to define, 386–390
- mail-routing loops, 35
- mail server, 37
- relaying by, 302
- 邮箱 server, 38
- mailbox for user, 14
- mailbox protocols, 22–29
- mailbox synchronization, 25
- maildrop keyword in user database, 155
- MAILER command (m4), 89, 92, 95, 98, 118–122, 363–390
- g generic-linux.mc file, 98, 118–122
- MAILER-DAEMON alias, 152
- MAILER (local) command (m4), 95, 119
- miler (m4) command, 205–211, 215
- MAILER (procmail) command (m4), 131, 168
- mailer rulesets, 224–226
- MAILER (smtp) command (m4), 95, 119
- quick reference, 361–366
- configuration file, 94. See also .m4 file
- building simple, 99–102
- installing, 100–102
- putting in place, 101
- sample, 97–99
- output control, 92–94
- reasons to use, 216
- macro variables, expanding, 184
