The first section of this chapter introduces the concept of security and defines some important terms that will be used throughout this book.

# # An Information Security Primer

There is nothing mystical about information security. At times overly glorified, and rarely well understood, the concept of information security cuts across many other disciplines, including network and system administration, programming, configuration management, and even documentation, auditing, and training. As a Linux server administrator, you will find that securing your network is an exercise in versatility. Very few corporations are large enough to justify the additional expense of having an information security expert on staff, and yet, practically all corporations would be adversely affected by even the most casual intrusion.

This section starts by defining a set of working terms commonly used when discussing information security and then moves on to define the process of information security, detailing each of the steps that make up this process.

# ## Security Terminology

Throughout this book, I will use several terms that are often not well understood, or that are open to interpretation. This section provides working definitions for these security-related concepts.

# ### Bastion Host

While the general aim of securing your network is to keep unauthorized personnel out of your servers, there is an increasing need to allow public access to some of these servers. At the very least, you will be asked to maintain a public Web and FTP server, and perhaps even a publicly available DNS server. A *bastion host* is one that should be publicly available enough that you don’t feel comfortable placing it in the same segment as your private servers. It’s a fortified host, hence the name. A bastion host is typically designed and maintained by the system administration staff who are knowledgeable about the security issues involved in setting up public servers such as these.