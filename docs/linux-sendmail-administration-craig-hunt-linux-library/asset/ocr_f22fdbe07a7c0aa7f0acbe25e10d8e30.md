While this book is intended to be read as a whole, I understand that many system administrators simply do not have the time to read an entire text. They must go to the topic in question and get a reasonably complete picture of the "why" as well as the "how" of that topic. To facilitate understanding, necessary background material is summarized where the topic is discussed and accompanied by pointers to the part of the text where the background material is more thoroughly discussed.

# Part 1: How Things Work Part 1 provides the information you need to understand how mail is moved across a network. Chapter 1 describes the protocols used to move the mail and Chapter 2 describes the architectural components that handle mail as it moves from its source to its destination. Chapter 3 describes installing and running the Sendmail program.

Chapter 1: Internet Mail Protocols Network protocols are needed to reliably mail from the sender to the receiver. This chapter explains the function and purpose of Simple Mail Transfer Protocol (SMTP), Multipurpose Internet Mail Extensions (MIME), Post Office Protocol (POP), and Internet Mail Access Protocol (IMAP).

Chapter 2: Understanding E-Mail Architecture Domain Name Servers, mailbox servers, and mail readers all play a role in delivering the mail. This chapter describes these components and how to use them to build your own e-mail architecture. The tasks performed by Sendmail in delivering the mail and the roles of POP and IMAP are explained.

Chapter 3: Running Sendmail The sendmail command and how and when it is invoked are covered, downloading, compiling, and installing Sendmail.

# Part 2: Essential Configuration Part 2 covers the basic configuration skills needed by every Sendmail administrator. It is composed of three chapters: Chapter 4, "Creating a Basic Sendmail Configuration," Chapter 5, "Understanding a Vendor's Configuration," and Chapter 6, "Using Sendmail Databases."

Chapter 4: Creating a Basic Sendmail Configuration Sendmail requires a configuration that is compatible with the version of Sendmail that is installed. The configuration is built from the m4 library delivered with the Sendmail source code distribution. This chapter explains how to build your own simple configuration with m4. A sample configuration is built step by step.

Chapter 5: Understanding a Vendor's Configuration Most Linux systems come with a default Sendmail configuration. This chapter explains that configuration, what it does, and what you have to do to provide the services you need with the default configuration. The generic Linux configuration delivered with the Sendmail source code and the Red Hat configuration are covered.