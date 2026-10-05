
# 432 Appendix C Sendmail Variables, Options, and Flags

## Table C.5 Mailer Flags

| Name | Function |
|---|---|
| C | Adds @domain to addresses that do not have an |
| D | Adds a Date: header line to outgoing mail. |
| E | Adds > to message lines that begin with From: |
| e | Indicates that this is a resource-intensive mailer. |
| F | Adds a From: header line to outgoing mail. |
| f | Indicates that this mailer allows trusted users to send mail under other names. |
| h | Preserves uppercase in hostnames. |
| I | Indicates that this mailer uses SMTP. |
| L | Limits the line length as required by RFC 821. |
| l | Indicates that this is a local mailer. |
| M | Adds a Message-Id: header line to outgoing mail. |
| m | Indicates that the mailer can send to multiple users in one transaction. |
| n | Indicates that Unix-style From: lines should not be used. |
| P | Adds a Return-Path: header to outgoing mail. |
| R | Uses the Mail From: return-path rather than the return address. |
| r | Indicates that this mailer allows trusted users to send mail under other names. |
| S | Prevents the user ID from being reset before calling the mailer. |
| s | Strips quotes off of the address before calling the mailer. |
| U | Indicates that the mailer requires Unix-style From: lines. |
| u | Preserves uppercase in usernames. |

## Table C.5 Mailer Flags (continued)

| Name | Function |
|---|---|
| X | Prepends a dot to lines beginning with a dot. |
| x | Indicates that the mailer wants a Full-Name: header line. |

# Index

Note to the reader: Throughout this index **boldface** page numbers indicate primary discussions of a topic. *Italicized* page numbers indicate illustrations.

## Symbols and Numbers

- - ! (exclamation point) for UUCP bang addressing, 188
- $: symbol in rewrite rules, 235–236
- @# symbol in rewrite rules, 235
- &cx syntax, 184
- $(database-spec$) syntax, 239
- #discard mailer, 244
- #error mailer, 244, 313
- $[hostname], 238
- >name syntax, 236–237
- to call rules, 221
- #OK mailer, 244
- $v command, 296
- . (dot character, 188–189, 228
- =M command, 291
- =S command, 291–292
- [bracket] character, 188–385
- 7bit encoding, 109
- 8bit encoding, 19
- 8BITIME, 21

- - access database, 156–161, 197
- action field in, 159–161
- address field in, 157–159
- address formats, 158
- to block mail, 309–312
- creation, 311–312
- linuxconf to create, 311, 312
- TLS actions in, 355
- access_db feature, 130, 132, 143, 157, 376, 388
- action field in access database, 159–161
- AddDomain rules, 225
- address field in access database, 157–159
- address test mode
- commands, 281
- configuration file, 290–291
- debug setting setting, 290–293
- alias
- defining personal mail, 153–154
- for e-mail recipient, 46
- in Sendmail, 47–48
- aliases database, 138, 149–154
- input address processing through, 271
- location for, 200
- preventing modification, 341
- for Red Hat, 150–151
- Sendmail instructions to rebuild, 126
- vs. user database, 155–156
- aliases file, 47

## A

- - acceptable use policy, 300
- accept_unqualified_senders feature, 376, 389
- accept_unresolvable_domains feature, 131, 306, 389

## AliasFile option in sendmail.cf – CANONIFY_DOMAIN command (m4)

- AliasFile option in sendmail.cf, 418
- ALIAS_FILE variable, 127, 130, 150
- AliasWait option in sendmail.cf, 418
- allmasquerade feature, 252, 376, 388
- AllowBogHELO option in sendmail.cf, 418
- always_add_domain feature, 129–130, 132, 377, 381, 390
- anonymous FTP to download RPM
- anti-spam rule definition, defining, 311
- APOP command (POP), 23, 329
- APPEND command (IMAP), 27
- application media type (MIME), 16
- arguments for m4 macros, quoted strings, 96
- ArgV (i), in mailer definition, 209, 211
- arithith database, definition, 197
- ASCII, e-mail support, 19
- asymmetric cryptography, 343
- audio media type (MIME), 16
- AUTH DIGEST-MD5, 22
- AUTH extension to SMTP, 344
- AUTH protocol, 342
- auth server (identd), 300
- AUTHENTICATE command (IMAP4), 26
- authentication, 343–344, 344–350
- in relaying, 349–350
- authentication client, 347–349
- authid (authentication identity), 347
- AuthMechanisms option in sendmail.cf, 418
- AuthOptions option in sendmail.cf, 418
- AutoRebuildAliases option in sendmail.cf, 418

## B

- - background daemon, longterm sendmail, 398
- backup mail exchange server, 344
- base64 encoding, 196
- bestmx_is_local feature, 377, 381, 390
- binary encoding, 19
- BIND software, 74
- domain database, 380
- domain feature, 143, 144, 171, 377
- .BITNET pseudo-domain, 125–126
- BITNET_RELAY variable, 125–126, 256, 386
- blacklist_recipients feature, 130–131, 132, 158–159, 377, 388
- BlankSub option in sendmail.cf, 418
- BSD-style Linux system, running on, 53
- buffers for sendmail.cf data, 93
- bug fixes, 326
- Build command, to compile sendmail, 72–73
- build script, in cl/cf directory, 87–88

## C

- - command, 188
- C[] command, 188
- C (define) command, 182, 186–190, 215
- CACERTFile option in sendmail.cf, 418
- CACPath option in sendmail.cf, 418
- Caldera, 54
- System-style Linux command, 290
- canonify ruleset, 44, 220, 222, 243, 280
- CANONIFY_DOMAIN command (m4), 362, 390

## CANONIFY_DOMAIN_FILE command (m4) - comments 437

- CANONIFY_DOMAIN_FILE command (m4), 362, 390
- CAPABILITY command (IMAP4), 26
- case sensitivity, 153, 173, 195
- certificate, 350
- self-signed, 352
- certificate authority, 352
- and public key, 350
- cf directory structure, 82–91
- cf/cf directory, 85–88
- contents, 86
- cf/cf directory, build script, 87–88
- cf/domain directory, 85
- cf/feature directory, 90
- cf/hack directory, 83–84
- cf/m4 directory, 90–91
- cf/mailer directory, 89
- cf/ostype directory, 88–89
- cf/autocon directory, 84
- cf file extension, 86
- cf.m4 file, 92
- cf.m4 file, 91
- changes, dealing with, 117
- Charset (C) field, in mail definition, 210
- CHECK (IMAP4), 27
- CheckAliases option in sendmail.cf, 418
- check_mail ruleset, 222
- CheckpointInterval in sendmail.file, 418
- check_re ruleset, 222, 223
- check_relay ruleset, 222, 223
- konfig, to enable Sendmail, 38
- class E, 118
- class M, 252
- class R, 146, 191, 302, 303
- class t, users in, 202
- class O, 188
- class P, 187–188
- class variables, 416–417
- loading from file, 190–191
- in pattern matching, 229
- class w, 127
- adding value to, 187
- failed test, 147–148
- class w variable, loading from file, 115–116
- classes in Sendmail, 186
- setting and viewing, 278–288
- ClassFactor option in sendmail.cf, 418
- ClassTest ruleset, 230
- cleanup after RPM software, 69–71
- client mail, 38
- problems from relay, 302
- Properties for configuring, 38–93
- sendmail, as, 49
- client-only.mc configuration file, 262
- client_add variable, placing in, 308
- ClientVertFile in sendmail.cf, 419
- ClientKeyFile in sendmail.cf, 419
- ClientPortOptions in sendmail.file, 419
- CLOSE (IMAP4), 27, 29
- ColonOkAddr option in sendmail.file, 419
- command-line options to test Sendmail, 269–280
- -bv option, 270–271
- hoststat command, 273–276
- mailq command, 276–280
- verbase option, 271–273
- comments m4 macro language, 94

## compatibility of Sendmail — Cyrus mailers

- in Red Hat aliases database, 151
- from script lines, 53
- in sendmail.cf file, 182
- compatibility of Sendmail configuration, 75–76
- confMAPDEF database, available options, 139
- confMAX_DAEMON_CHILDREN parameter, 335–336
- confMAX_HEADERS_LENGTH variable, 132
- confMAX_MESSAGE_SIZE, 337
- confSERVER_CERT parameter, 351
- confSERVER_KEY parameter, 351
- confCTO_CONNECT variable, 126, 132
- confTRUSTED_USER parameters, 202
- confFR_NULL_MX_LIST variable, 126–127, 132
- USERDB_SPEC variable, 127, 132, 142, 154
- compiling Sendmail with Build command, 72–73
- checking options, 141
- conditionals in D (define macro) command, 185–186
- in m4 macro language, 110
- in pattern matching, 231
- in promaile script, 317
- confAUTH_MECHANISMS parameter, 345
- confAUTO_REBUILD variable, 126, 132
- confBINDIR parameter, 110
- confCLIENT_CERT parameter, 351
- confCLIENT_KEY parameter, 351
- confCONNECTION_RATE_THROTTLE, 336–337
- confCR_FILE variable, 146
- confCW_FILE variable, 115
- confDEF_USER_ID variable, 125, 338
- confDONT_PROBE_INTERFACES variable, 127, 132
- confEBINDIR variable, 128
- confORWARD_PATH variable, 113–114
- confHOST_STATUS_DIRECTORY, 273, 274
- config keyword for Sendmail error code, 244
- configuration file. See also sendmail.cf
- build script to create multiple, 88
- forcing reload, 59
- configuration variables for sendmail.cf file, 96
- confLDAP_DEFAULT_SPEC, 394
