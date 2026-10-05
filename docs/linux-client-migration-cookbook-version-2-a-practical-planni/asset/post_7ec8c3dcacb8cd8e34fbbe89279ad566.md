provides a great example of how the flexibility of the desktop Linux software stack facilitates innovative deployment models that consolidate client computing systems.

- Finally, once you have settled on the design and configuration of your Linux-based operating system image, and you have designed and tested a cost-effective deployment model that optimizes projected management costs, then you still have to migrate your users to the new systems. One key challenge in minimizing the disruption to users is this: how do you efficiently capture and migrate the set of important desktop personalization data from existing Windows clients to the target Linux clients? Tools for automating migration of this data are now available from multiple vendors. We highlight the importance of using these tools in a medium-to-large enterprise, and provide a deep dive introduction to how you can use one of these tools, in Appendix C, "Automating desktop migration with Versora Desktop Description" on page 277.

## The team that wrote this redbook

Version 2 of this IBM Redbook was produced by a team of specialists from around the world working at the International Technical Support Organization, Austin Center.

Chris Amend is a Project Leader and IT Architect based in the Austin, Texas ITSO center. He has a total of 15 years of IT industry experience, including the last five with IBM. His experience includes UNIX/Linux systems engineering, network engineering, Lotus®Domino®-based content management solutions, and WebSphere Portal-based solution design.

Jeroen van Hof is a Senior IT Specialist with IBM Global Services in the Netherlands. He has over 15 years of experience with UNIX operating systems and over 10 years experience with Linux. Before joining IBM through PwC, worked in high-performance computing at the Dutch National Supercomputing Centre as a parallelisation expert. His areas of expertise include UNIX/Linux, Windows, Virtualization, TCP/IP networking (routing, switching), parallelisation (MPI, PVM), firewall security, programming (Fortran, C, Pascal, Perl), SAP Basis consultancy, and Web technologies (HTTP, HTML, CGI). He is a Red Certified Engineer, VMware Certified Professional and SAP Certified Technology Consultant. He has a PhD in Theoretical Physics from the University of Nijmegen.

Nick Lassonde is the Chief Software Architect at Versora, where he leads development activities on Progression Desktop, a leading automation tool for migrating personalization data between Windows and Linux desktop environments. Prior to Versora, Nick was Senior Architect for Miramar Systems, where he focused primarily on development of tools for moving critical data and configurations of automated testing procedures. Prior to Miramar, Nick served as a Software Architect for Cadence Design Systems, where he focused on interoperability issues between Microsoft and Linux/UNIX® workstations.

Ben Li is the Vice-President of Innovation and Outreach at Useful Corporation, where he oversees development of integrated software and hardware solutions for multi-station Linux systems. His technical experience includes management roles in security and system administration on Linux, Windows and OS X operating systems in academic environments, developing and refining content management systems and workflows, as well as online and cross-media publishing. Ben is also a researcher for The Center for Innovation Studies, Calgary-based research and advocacy group for the innovation and research commercialization community, and holds two degrees from the University of Calgary. As a consultant prior to joining Useful, Ben has developed a helpdesk notification system for a multi-national business services corporation, as well as a database-driven public relations tracking and reporting system for a leading Canadian energy company.

Kurt Taylor is a Senior Software Engineer at the IBM Linux Technology Center, located in Austin, Texas. Kurt is currently a Technical Leader for the Linux System Management Team. He has worked at IBM for 10 years, and has over 17 years of industry experience architecting, designing and developing distributed network and system management products. He is currently working with the OpenPegasus project and the OSDL Desktop Linux workgroup. Kurt graduated from the University of North Texas with a Bachelor of Science degree in Computer Science.

## Acknowledgements

This is the second version of this IBM Redbook. The IBM Redbook team would like to acknowledge and the team of authors who wrote the first version of this book: Chris Almond, Art Cannon, Jeroen van Hof, Christian Patsch, Sekkar Vaddadi, Oliver Mark, and Thomas Schaller. Their efforts in the first version helped to create the original concept for this book, and lay down a significant amount of content that still appears in the second version.

In addition, the team would like to thank the following people for providing significant support for this project:

- Greg Kelleher, Senior Program Manager Worldwide Linux Desktop Strategy and Market Development: For sponsoring the project and helping to guide the development of the content outline and scope for the book.

- Stephen Hochstettler, ITSO Project and Linux Team Leader: For his vision and support.

- John Bergland, ITSO Project Leader, Lotus and WebSphere Portal, for his contributions.

- Bernard Golden, for his contributions.

- Gerry Anderson, Jim Zemlin, and Dirk Hohndel, Intel Inc.

- Mike Sheffey, Jon Walker, Versora Inc., and Timothy Griffin, Useful Inc.

- Gerry Rivers, Jonathan Blandford, Chris Blizzard, Dan Walsh, Nickell, and Máirin Duffy, Red Hat, Inc.

- IBM ITSO Professionals: Erica Wazewski (legal support), and Leslie Parham for her support in preparing the book for publication

## Become a published author

Join us for a two-to-six-week residency program! Help write an IBM Redbook dealing with specific products or solutions, while getting hands-on experience with leading-edge technologies. You'll team with IBM technical professionals, Business Partners and customers.

Your efforts will help increase product acceptance and customer satisfaction. As a bonus, you'll develop a network of contacts in IBM development labs, and increase your productivity and marketability.

Find out more about the residency program, browse the residency index, and apply online at:

http://ibm.com/redbooks/residencies.html

## Comments welcome

Your comments are important to us!

We want our Redbooks™ to be as helpful as possible. Send us your comments about this or Redbooks in one of the following:

- Use the Contact us review redbook form found at:

- http://www.redbooks.ibm.com/

- Send your comments in an Internet note to:
* redbook@us.ibm.com

- Mail your comments to:
IBM Corporation, International Technical Support Organization
Bldg 905, 3D-004
11400 Burnet Road
Austin, Texas 78758-3493

## Part 1

## Choosing Linux

Part 1 of this book includes:

- Chapter 1, “Introduction” on page 1
- Chapter 2, “The case for migration” on page 25

## Introduction

For several years now, many people involved with computing and the Internet have harbored hopes that Linux might become a viable user operating system choice for a broader segment of general purpose users. At the same time, there has been growing frustration with the problems and limitations of the current dominant commercial desktop operating system offerings from Microsoft. In turn, this frustration has fueled a greater need in the market for alternative desktop operating system choices. At the same time, Linux-based desktop-oriented distributions have improved tremendously as a result of the inclusive and open-ended dynamics of the open source development movement.

The goal of this book is to provide a technical planning reference for IT organizations large or small that are now considering a migration to Linux-based personal computers. For Linux, there is a tremendous migration of "how to" information available that addresses specific and very technical operating system configuration issues, platform-specific installation methods, user interface customizations, and more. This ebook includes some technical "how to" well, the overall focus of the content in this book is to walk the reader through the important considerations and planning issues you could encounter during a migration project. Within the context of a pre-existing Microsoft Windows-based environment, we attempt to present a more holistic, end-to-end view of the technical challenges and methods necessary to complete a successful migration to Linux-based clients.
