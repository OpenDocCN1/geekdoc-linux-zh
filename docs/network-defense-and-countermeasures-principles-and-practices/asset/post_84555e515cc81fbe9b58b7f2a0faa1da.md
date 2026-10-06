
# Dedication

This book is dedicated to all the people working in the computer security field, diligently working to make computer networks safer.

# Acknowledgments

While only one name goes on the cover of this book, it is hardly the work of just one person. I would like to take this opportunity to thank a few of the people involved. First of all, the editing staff at Pearson worked extremely hard on this book. Without them this project would simply not be possible. I would also like to thank my wife, Teresa, for all her support working on this book. She is always very supportive in my endeavors, a one-woman support team!

# About the Technical Reviewers

Akhil Behl, CIE No. 19564, is a passionate IT executive with key focus on cloud and security. He has more than 15 years of experience in the IT industry working in several leadership, advisory, consultancy, and business development profiles with various organizations. His technology and business specialization includes cloud, security, infrastructure, data center, and business communication technologies.

Akhil has authored multiple titles on security and business communication technologies. He has contributed as technical editor for a number of books on network and information security. He has published several research papers in national and international journals, including IEEE Xplore, and presented at various IEEE conferences, as well as other prominent ICT, security, and telecom events.

Cecil also holds CCSK, CHFI, PMP, ITIL, VCP, TOGAF, CEH, ISM, and several other industry certifications. He has a bachelor's in technology degree and an MBA.

Steve Kalman is both an attorney and a professional security expert. He holds the following credentials from (ISC)2 for whom he worked as an authorized instructor: CISSP, CCFP-US, CSSLP, ISSMP, ISSAP, HCISSP, SSCP. Steve has been author or technical editor for more than 20 Pearson/Cisco Press books.

# We Want to Hear from You!

As the reader of this book, you are our most important critic and commentator. We value your opinion and want to know what we're doing right, what we could do better, what areas you'd like to see us publish in, and any other words of wisdom you're willing to pass our way.

We welcome your comments. You can email or write to let us know what you did or didn't like about this book—as well as what we can do to make our books better.

Please note that we cannot help you with technical problems related to the topic of this book.

When you write, please be sure to include this book's title and author as well as your name and email address. We will carefully review your comments and share them with the author and editors who worked on the book.

Email: feedback@pearsonitcertification.com

Mail: Pearson IT Certification

ATTN: Reader Feedback
800 East 96th Street
Indianapolis, IN 46240 USA

# Reader Services

Register your copy of Network Defense and Countermeasures at www.pearsonitcertification.com for convenient access to downloads, updates, and corrections as they become available. To start the registration process, go to www.pearsonitcertification.com/register and log in or create an account*. Enter the product ISBN 9780789759962 and click Submit. When the process is complete, you will find any available bonus content under Registered Products.

*Be sure to check the box that you would like to hear from us to receive exclusive discounts on future editions of this product.

# Chapter 1

# Introduction to Network Security

# Chapter Objectives

After reading this chapter and completing the exercises, you will be able to do the following:

- Identify the most common dangers to networks.
- Understand basic networking.
- Employ basic security terminology.
- Find the best approach to network security for your organization.
- Evaluate the legal issues that will affect your work as a network administrator.
- Use resources available for network security.

# Introduction

Finding a week without some major security breach in the news is difficult. University web servers hacked, government computers hacked, banks’ data compromised, health information exposed—the list goes on. It also seems as if each year brings more focus to this. Finding anyone in any industrialized nation who had not heard of such things as websites being hacked and identities stolen would be difficult.

More venues for training also exist. Many universities offer Information Assurance degrees from the bachelor’s level up to the doctoral level. A plethora of industry certification training programs are available, including the CISSP, EC Council’s CEH, Mile2 Security, SANS, and CompTIA’s Security+. There are also a number of universities offering degrees in cyber security, including distance learning degrees.

Despite this attention from the media and the opportunities to acquire secure training, far too many computer professionals—including a surprising number of network administrators—do not have a clear understanding of the type of threats to which network systems are exposed, or which ones are most likely to actually occur. Mainstream media focuses attention on the most dramatic computer security breaches rather than giving an accurate picture of the most plausible threat scenarios.

This chapter looks at the threats posed to networks, defines basic security terminology, and lays the foundation for concepts covered in the chapters that follow. The steps required to ensure the integrity and security of your network are methodical and, for the most part, already outlined. By the time complete this book, you will be able to identify the most common attacks, explain how they are perpetrated to prevent them, and understand how to secure your data transmissions.

# The Basics of a Network

Before diving into how to protect your network, exploring what networks would probably be a good idea. For many readers this will be a review, but for some it might be new material. Whether this is a review for you, or new information, having a thorough understanding of basic networking before attempting to study network security is critical. Also, be aware this is just a brief introduction to basic networking concepts. Many details are not explored in this chapter.

A network is simply for machines/computers to communicate. At the physical level, it consists of all the machines you want to connect and the devices you use to connect them. Individual machines are connected either with a physical connection (a category 5 cable going into a network interface card, or NIC) or wirelessly. To connect multiple machines together, each machine must connect to a hub or switch. In larger networks, each subnet is connected to the others by a router. We look at many attacks in this book (including several in Chapter 2, "Types of Attacks") that focus on the devices that connect together on a network (that is, routers, hubs, and switches). If you find this is not enough, this resource might assist you: http://comnetworking.about.com/od/basicnetworkingconcepts/Networking_Basics_Key_Concepts_in_Computer_Networking.htm.

# Basic Network Structure

Some connection point(s) must exist between your network and the outside world. A barrier is set up between your network and the Internet, usually in the form of a firewall. Many attacks discussed in this book work to overcome the firewall and get into the network.

The real essence of networks is communication—allowing one machine to communicate with another. However, every avenue of communication is also an avenue of attack. The first step in understanding how to defend a network is having a detailed understanding of how computers communicate over a network.

The previously mentioned network interface cards, switches, routers, hubs, and firewalls are the fundamental physical pieces of a network. The way they are connected and the format they use for communication is the network architecture.
