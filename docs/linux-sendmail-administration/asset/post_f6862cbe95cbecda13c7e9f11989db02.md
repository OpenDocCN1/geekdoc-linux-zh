
# Contents xiii

- Address Masquerading. . . . . . . . . . . . . . . . . 249
- Enabling Masquerading . . . . . . . . . . . . . . . . . 249
- Masquerade Options . . . . . . . . . . . . . . . . . 251
- Masquerading Usernames . . . . . . . . . . . . . 256
- Writing Local Rules . . . . . . . . . . . . . . . . . 258
- Configuring a Relay Client. . . . . . . . . . . . . . 261
- In Sum . . . . . . . . . . . . . . . . . . . . . . 265

# Part 4 Maintaining a Healthy Server 267

- Chapter 10 Testing Sendmail . . . . . . . . . . . . 269
- Simple Command-bv Option . . . . . . . . . . . . 269
- Using the -bv Option . . . . . . . . . . . . 270
- Running in Verbose Mode . . . . . . . . . . . . 271
- The hoststat Command . . . . . . . . . . . . 273
- The mailq Command . . . . . . . . . . . . 276
- Running Sendmail in Test Mode . . . . . . . 280
- Testing with the /parse Command . . 283
- Processing a Specific Address Type . . 284
- Testing with the /try Command . . . . . 285
- Displaying and Setting Internal Values . 287
- Using Debug Levels . . . . . . . . . . . . 293
- In Sum . . . . . . . . . . . . . . . . . . . . . 298
- Chapter 11 Stopping Spam . . . . . . . . . . . . 299
- Don't Be a Spam Source . . . . . 299
- Define an Acceptable Use Policy . . . 300
- Run the Identification Daemon. . . . 300
- Properly Configure Mail Relaying. . 301
- Use Sendmail to Block Spam. . . . 305
- Using the Realtime Blackhole List. . 306
- Using the access Database . . . 309
- Using Anti-Spam Rewrite Rules . . 312

# xiv Contents

- Filtering Out Spam at the Mailer . . . . . . . . . . . . 314
- Managing Mail with procmail. . . . . . . . . . . . . 315
- In Sum. . . . . . . . . . . . . . . . . . . . . . . . . 319

# Chapter 12 Sendmail Security . . . . . . . . . . . . 321

- Basic Security . . . . . . . . . . . . . . . . . . . . 322
- Secure the Hardware . . . . . . . . . . . . . . . . . . 322
- Secure the Software. . . . . . . . . . . . . 324
- Limit Login Access . . . . . . . . . . . . . . . . . 328
- Securing a Sendmail Server. . . . . . . . . . . . . . . . 335
- Securing Sendmail against Unauthorized Access . . 337
- Sendmail Security Protocols . . . . . . . . . . . 342
- Encryption and Cryptography . . . . . . . . . . 343
- Sendmail Authentication . . . . . . . . . . . 344
- Transport Layer Security . . . . . . . . . . . 350
- In Sum. . . . . . . . . . . . . . . . . . . . . . 356

# Appendices

# Appendix A m4 Macro Command Reference . . . . . . . . . . . 361

- Complete Command Reference . . . . . . . . . . . . 366
- define . . . . . . . . . . . . . . . . . . . 367
- FEATURE . . . . . . . . . . . . . . . . . . . 376
- OSTYPE. . . . . . . . . . . . . . . . . . . 382
- DOMAIN . . . . . . . . . . . . . . . . . . . 386
- MAILER . . . . . . . . . . . . . . . . . . . 390
- Local Code . . . . . . . . . . . . . . . . . . 392
- DAEMON_OPTIONS. . . . . . . . . . 393
- LDAP Mail Routing . . . . . . . . . . . 394

# Appendix B The sendmail Command . . . . . . . . . . . . 395

- Command-Line Switches. . . . . . . . . . . . . 396
- Debug Levels . . . . . . . . . . . . . . 399

# Appendix C Sendmail Variables, Options, and Flags . . . . . . . . . . . 411

- Variables . . . . . . . . . . . . . . . . . . . 411
- Class . . . . . . . . . . . . . . . . . . . 416
- Options . . . . . . . . . . . . . . . . . . . 418
- Mailer . . . . . . . . . . . . . . . . . . . 431
- Index . . . . . . . . . . . . . . . . . . . 435

This page intentionally left blank

# Introduction

Electronic mail is one of the most fundamental services today can provide. Because of this, its reliability must be high. First, of course, we must understand the underlying system. Sendmail is designed for Linux, and we focus on what is important to build a server. No, matter how well you thought out or how long, can provide accurate examples for every situation. This book provides you with the information you need to develop the correct solution for your situation on your own.

# Who Should Buy This Book

This book is for anyone who is building a network server using Linux. The book doesn't assume that you know much about Sendmail, but it does assume that you have a good understanding of computers and networks. If you feel that you need to brush up on these topics, start with Linux Administration by Vicki Stanfield and Roderick W. Smith (2001).

Linux system administrators will find this invaluable as their primary resource for Sendmail. It provides detailed instruction on how a mail server is built on a Linux platform. Security features specific to Linux are covered. Information about Linux that is overlooked by other books is provided. Even administrators of Unix systems will find this book a useful companion. This book provides a detailed description of the underlying Internet protocols and ties that discussion to configuring Sendmail. It provides this information in a clear and organized manner. The insights into how e-mail works and why certain configuration values are used will be helpful to anyone running Sendmail—even if they don't use Linux.

# How This Book Is Organized

This book is divided into five parts: “How Things Work,” “Essential Configuration,” “Advanced Configurations,” “Maintaining a Healthy Server,” and Appendices. The five parts are composed of twelve chapters and three appendices.

A reader who understands the fundamentals of the mail protocols and architecture can jump to the Essential Section. An experienced administrator who understands basic Sendmail configuration can jump to the Advanced Configuration part of the book. However, the book was designed as a unit and was meant to be read as a whole, and many chapters reference material covered in other chapters. The book starts with foundation material that explains the underlying system, moves through essential configuration skills that every system administrator needs, and then concludes with specialized configurations that are needed for special situations. Most system administrators will benefit from reading the entire text.
