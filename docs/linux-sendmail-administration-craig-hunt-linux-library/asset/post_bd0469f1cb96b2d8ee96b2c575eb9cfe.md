
# Acknowledgments

I have now written my third book for Syex, who, frankly, I never thought happen. I thought writing Linux Network Servers 24seven, my first book for Syex, would be a one-shot deal. But then came the opportunity to write a series of books all focused on Linux. As much as I love writing, I love writing about Linux even more. To add to the joy of this project, the people at Syex have been wonderful. Like the other books, one has been written with the support of some excellent people.

I have been surprised by the consistent quality of the people I work with because the cast of characters has changed. It is perfectly normal for different books to have different editors, but fate has a bigger player in these changes than management. Guy Hart-Davis, the Associate Publisher who first listened to my proposals for this library, inherited a large home in England and went off to be “Lord of the Manor.” (Like everyone else at Sy, I’m dying to go to England to visit him.) By great luck, Neil Eddie took over as Associate Publisher for the Linux Library. Liz is the person who introduced me to Syex. She was the first person to hear my ideas about the Linux Library and to encourage me to propose them to Syex. I couldn't have a better partner than Neil.

Maureen Adams, who started as the Acquisition Editor for this, has been promoted to Mom. She left the project to give birth to Emma. Instead of baby-sitting, she is sitting with a real baby. I’d call that a major promotion!

Tom Crit, who took over as Acquisition Editor, is a career publishing professional. Tom’s no-nonsense style helps him deal with me and the other authors in the Craig Hunt Linux Library. Tom deserves special thanks for understanding that the technical quality and not the production schedule was the most important factor in creating this library.

The Production Editor for this book was Liz Burke—many thanks to Liz for her flexibility in working around my schedule. Suzanne Goraj was the Editor. I want to thank for respecting my writing style while still doing a good job of improving my grammar. Randy Russell and Eric Gnett were the Technical Editors. Their suggestions were very helpful in creating a more accurate book. Randy has a particularly fine eye for technical details.

I would like to thank all of the production people and artists for their work: Nila Nichols, Jennifer Campbell, Nancy Guernsey, Nelson Kim, Yariv Rabinovich, Nanette Duffy, Nancy Riddough, Laurie O’Connell, and Andrew Fox.

I’d also like to thank Karen Rman of KJ Design in Washington, D.C. Karen is a professional photographer and designer. I can attest to the fact that she is one of the best. Only the best of photographers could make my mug look presentable enough for the cover of a book.

Twelve-hour days. No vacations. Not even weekends off. When the schedule gets tight and deadlines loom, I’m not the easiest person to live with. Kathy, thanks for living with me.

# Contents at a Glance

Introduction . . . . . . . . . . . xvii

## Part 1 How Things Work 1

- Chapter 1 Internet Mail Protocols . . . . . . . . 3
- Chapter 2 Understanding E-Mail Architecture . . . . . . . 31
- Chapter 3 Running Sendmail . . . . . . . . . . . 51

## Part 2 Essential Configuration 79

- Chapter 4 Creating a Basic Sendmail Configuration . . . . . 81
- Chapter 5 Understanding a Vendor’s Configuration . . . . . 107
- Chapter 6 Using Sendmail Databases . . . . . . . . . . 137

## Part 3 Advanced Configuration 177

- Chapter 7 sendmail.cf File . . . . . . . . . . . . 179
- Chapter 8 Understanding Rewrite Rules . . . . . . . . 219
- Chapter 9 Special m4 Configurations . . . . . . . . . . 247

## Part 4 Maintaining a Healthy Server 267

- Chapter 10 Testing Sendmail . . . . . . . . . . . 269
- Chapter 11 Stopping Spam . . . . . . . . . . . . 299
- Chapter 12 Sendmail Security . . . . . . . . . . . 321

## Appendices 359

- Appendix A m4 Macro Command Reference . . . . . . . . 361
- Appendix B The sendmail Command . . . . . . . . . . 395
- Appendix C Sendmail Variables, Options, and Flags . . . . . . 411

Index . . . . . . . . . . . . . . . . . . . 435

# Contents

- Introduction . . . . . . . . . . . . . . . . . . . . . . xvii
- Part 1 How Things Work . . . . . . . . . . . . . . . . 1
- Chapter 1 Internet Mail Protocols . . . . . . . . . . . . 3
- The Internet Protocol Suite . . . . . . . . . . . . . . 4
- A Simple Mail Transport Protocol . . . . . . . . . . 4
- Using SMTP through *telnet* . . . . . . . . . . . . . 6
- SMTP Response Codes . . . . . . . . . . . . . . . . 9
- Observing SMTP with Verbose Mode . . . . . . 11
- A Basic Mail Message . . . . . . . . . . . . . . 13
- Message Headers . . . . . . . . . . . . . . . . 13
- Multipurpose Internet Mail Extensions . . . . 15
- The Content-Type Header . . . . . . . . . . . 16
- The Content-Transfer-Encoding Header . . 19
- Extended SMTP . . . . . . . . . . . . . . . 20
- Extended Service Keywords . . . . . . 21
- Mailbox Protocols . . . . . . . . . . . . 22
- Post Office Protocol . . . . . . . . . . . 22
- Internet Mail Access Protocol . . . . . 25
- In Sum . . . . . . . . . . . . . . . . . 29
- Chapter 2 Understanding E-Mail Architecture . . . 31
- The Role of DNS . . . . . . . . . . . . 33
- Observing MX Records . . . . . . . . . 35
- The Components of Architecture . . . . . . . . 36
- The Definitions . . . . . . . . . 36
- The Sample Architectures . . . . . . . . 39
- The Submission Agent . . . . . . . . . . 41
- The Transfer Agent . . . . . . . . . . 42
- The Client . . . . . . . . . . 46
- In Sum . . . . . . . . . . . . . 49
- Chapter 3 Running Sendmail . . . . . . . . . . . 51
- Running Sendmail Up . . . . . . . . . . . . 53
- The BSD-style System . . . . . . . . 54
- The V-style System . . . . . . . . 59
- Controlling Sendmail with Signals . . . . . . . . 61
- Installing Sendmail with dekg . . . . . . . . . . 61
- The de-style Configuration . . . . . . . . 66
- Installing Sendmail with RPM . . . . . . . . 68
- The RPM-style Configuration . . . . . . . . 71
- Installing Sendmail after . . . . . . . . . . . . 74
- The Problems . . . . . . . . . . 75
- The Compatibility . . . . . . . . . . . . 76
- Chapter 4 Creating a Basic Sendmail Configuration . . . . . 81
- The cf Structure . . . . . . . . . . . 83
- The Little-Used Directories . . . . . . . . . 85
- The domain Directory . . . . . . . . . . 85
- The ostype Directory . . . . . . . . . . 88
- The mailer Directory . . . . . . . . . 89
- The feature Directory . . . . . . . . . 90
- The m4 Language . . . . . . . . 90
- The m4 Output . . . . . . . . 92
- The Basic Commands . . . . . . . . 94
- The Sample m4 Configuration . . . . . . . 97
- The Simple m4 Configuration . . . . . . . . 99
- The More m4 Commands . . . . . . . . . 102
- In Sum . . . . . . . . . . . . . 105
- Chapter 5 Understanding a Vendor’s Configuration . . . . . 107
- The Generic Configuration . . . . . . . . . . . 108
- The OSTYPE File . . . . . . . . . . 109
- The DOMAIN File . . . . . . . . . . . 112
- The relay-domain . . . . . . . . . . 114
- Protecting the root Account from Masquerading . . . . . . 115
- The Essential Mailers . . . . . . . . . . . 117
- The Red Hat Configuration . . . . . . . . . . . 122
- Modifying the Red Hat Configuration . . . . . . . . . 131
- In Sum . . . . . . . . . . . . . . . . 135
- Chapter 6 Using Sendmail Databases . . . . . . . . . . 137
- Adding Database Support . . . . . . . . . . . . 138
- Database Compiler Options . . . . . . . . . . . 138
- Configuration Options . . . . . . . . . . . . 142
- The Cr, Cw, and Ct Files . . . . . . . . . . . 144
- The relay-domains File . . . . . . . . . . . 145
- The local-host-names File . . . . . . . . . . 147
- The aliases Database . . . . . . . . . . . . 149
- Defining Personal Mail Aliases . . . . . . . . . . 153
- The User Database . . . . . . . . . . . . . 154
- The access Database . . . . . . . . . . . . . 156
- The Address Field . . . . . . . . . . . . . . 157
- The Action Field . . . . . . . . . . . . . . . 159
- The virtuetable . . . . . . . . . . . . . . 161
- Defining a Virtual Domain . . . . . . . . . . . 161
- Defining virtuetable Delivery Addresses 163
- The mailtertable . . . . . . . . . . . . . . 166
- The genericstable . . . . . . . . . . . . . . 169
- Little-Used Databases . . . . . . . . . . . . 171
- The makemap Command . . . . . 172
- In Sum . . . . . . . . . . . . . . . . 174
