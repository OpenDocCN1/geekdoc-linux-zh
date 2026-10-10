
## 13. Which of the following requirements must be met to use NetStorage on a client computer? (Choose all that apply.)
- a. The NetStorage client software must be downloaded and installed on the client.
- b. The date and time settings must be close to the server's date and time.
- c. NetStorage must be installed on the server.
- d. The context for user accounts must be specified during NetStorage installation.

## 14. To change the configuration of NetStorage, you need to reinstall it. True or False?

## 15. Which of the following provides a collaborative computing environment for users to exchange and share information?
- a. iFolder
- b. NetStorage
- c. Virtual Office
- d. Web Manager

## 16. Novell Virtual Office can provide access to which of the following functions? (Choose all that apply.)
- a. Calendar
- b. iFolder
- c. iPrint
- d. NetStorage
- e. eGuide

## 17. Novell Virtual Office requires Novell Client to be installed on user computers. True or False?

## 18. Which of the following iFolder Management options do you use to set the context for LDAP to search for user accounts?
- a. Global Settings: General window
- b. Global Settings: User LDAPs window
- c. User Management window
- d. System Monitoring window

## 19. What is the default disk quota for iFolder user files?
- a. 1 GB
- b. 200 MB
- c. 500 MB
- d. 100 MB

## 20. Which of the following drive mappings appears in a user's NetStorage view? (Choose all that apply.)
- a. user home directory
- b. container login script drive mappings
- c. user login script drive mappings
- d. iFolder

# CASE PROJECTS

![](img/840007e8f98ea6653e5877e945c27dc6_456_0.png)

## Case Project 10-1: Planning OneNet Use, Scenario 1

Universal AeroSpace recently acquired a small machining company named ACER Tools that makes high-tensile parts for use on the Mars Rover. This company has five computers that need access to the Engineering NASA directory over a WAN. The employees will be on the road and need access to files as they travel. Which Novell OneNet technology described in this chapter best meets the needs of users in the ACER Tools company, and why?

![](img/840007e8f98ea6653e5877e945c27dc6_456_1.png)

## Case Project 10-2: Planning OneNet Use, Scenario 2

Some Engineering users are traveling to ACER Tools and need access to their personal files from computers at both the UAS home office and the ACER Tools facility. Which Novell OneNet technology described in this chapter best meets the needs of these users, and why?

# HANDS-ON PROJECTS

![](img/840007e8f98ea6653e5877e945c27dc6_456_2.png)

## Hands-on Project 10-1: Using NetStorage

A real test of the NetStorage service came when Eric went on a trip to a NASA space station contractor and wanted to download some CAD drawings for engineers to analyze. In this project, you simulate this situation by performing the following steps:

- 1. Log in with your administrative user name and password.
- 2. If necessary, create a user named **DHeise** in your Mgmt OU.
- 3. If necessary, create a user login script for your DHeise user that maps a drive to the Engineer directory.
- 4. Give your DHeise user the Read right to the Engineer directory.
- 5. Use the Paint program to create a simple drawing of a spaceship, and save it in your NASA directory as **SupplyVessel.bmp**.
- 6. Log out.
- 7. Log on to your local Windows system, clicking to select the **Workstation Only** check box.
- 8. Start your Web browser and access the NetStorage page.
- 9. Log in as the **DHeise** user.
- 10. Access the drive mapping to the Engineer directory, and then open the **SupplyVessel.bmp** file.
- 11. Demonstrate your results to your instructor.

![](img/840007e8f98ea6653e5877e945c27dc6_456_3.png)

## Hands-on Project 10-2: Using Virtual Office

The Engineering Department needs to collaborate on a new project to send a robot to the moon as research into a possible lunar base. In this project, create a Virtual Team consisting of all users in the Engineering OU. Test the Virtual Team by logging in as one of the members and placing an entry in the team calendar.

# CHAPTER 11
## IMPLEMENTING AND SECURING INTERNET SERVICES

> After reading this chapter and completing the activities,
> you will be able to:
> - Describe Novell’s Web Services and Net Services
> - Install and configure Web Services components
> - Describe technologies for securing Web services, including firewalls and virus protection
> - Explain encryption security techniques, Novell Certificate Services, and OpenSSH
> - Describe Novell’s backup services

As you have learned, Novell’s OneNet strategy uses the Internet to make network services and information available from anywhere at any time. To secure and support the OneNet features of Open Enterprise Server (OES), network administrators need to understand the components that make Internet services available on a NetWare 6.5 server; they also need to know how to implement these services and secure them from unauthorized access and attacks.

In addition to Internet services, OES includes Web and FTP services that can be installed and configured to deliver information to the Internet. In this chapter, you learn about the Internet service components in NetWare 6.5 and how to use them to provide Web services and secure a network against unauthorized access.

# INTRODUCTION TO NOVELL INTERNET SERVICES

Novell Internet and intranet services simplify setting up business networks by providing a common set of services for accessing data and resources with a variety of computer and server OSs. The NetWare 6.5 Internet service components can be divided into Net Services and Web Services components, as shown in Figure 11-1.

![](img/840007e8f98ea6653e5877e945c27dc6_459_0.png)

**Web Services** are TCP/IP-based applications that make network data and services, such as Web sites and FTP servers, available to users. To access a Web service, users need the correct client software running on their computers. For example, a Web browser, such as Internet Explorer or Netscape, is needed to access a Web site.

**Net Services** components extend the capabilities of standard Web services and include many of the services you have worked with already, such as iFolder, NetStorage, iPrint, iManager, and Remote Manager. As shown in Figure 11-1, a network can be configured so that requests for Net Services originating at users' computers are sent via the Internet through a firewall running on a server or router. After being checked through the firewall, the request is routed to a service based on its IP address and port number. IP addresses are used to direct a packet to the correct computer; port numbers are used to transfer the packet's information to the correct application. When an application starts, it provides TCP/IP with its port number. When a packet is received at a computer, the TCP/IP protocol stack uses the port number to determine which application running on the computer should get the packet's information. Table 11-1 lists commonly used applications and their default port numbers.

Table 11-1 Commonly used port numbers

| Port Number | Application |
| :--- | :--- |
| 21 and 22 | FTP |
| 23 | Telnet |
| 25 | SMTP (e-mail protocol) |
| 80 | Web server |
| 100 | Post Office Protocol (POP) |

To gain access to NetWare files and resources, Net Services run as applications on Web Services components, such as Apache Web Server. Novell chose Apache Web Server to host Net Services components because it's open-source Web server software, meaning it's freely available and can be modified to run on other OS platforms. By running through Apache Web Server, Novell Net Services can be set up on any network operating system (NOS) that supports Apache Web Server, including UNIX, Linux, Windows 2000 Server, and Windows Server 2003. In addition to processing requests for Net Services, Web Services components can make data available through Novell Portal Services. In the following sections, you learn about Web Services components and how Novell Portal Services can be used to customize Web access.

## Apache Web Server for NetWare

Apache Web Server is open-source Web server software originally developed by the Apache Group, a nonprofit organization. Currently, more than 60% of all Web-hosting organizations use Apache Web Server; because it's such a common platform for Web-based services, Novell made Apache Web Server an integral part of Open Enterprise Server Internet services. Apache Web Server is used in two ways on Open Enterprise Server. One instance of Apache is used to support Novell Net Services, such as iFolder, and is installed by default during NetWare 6.5 server installation. All configuration files for this Admin instance of Apache Web Server are in the SYS:\Adminsrv directory. Because of Apache Web Server's tight integration with Novell Net Services, it requires no special configuration by the network administrator. Apache Web Server is used by these NetWare 6.5 Web-based services:

- NetWare Web Manager
- NetWare Web Search Server
- NetWare WebAccess
- iPrint
- iFolder
- iManager

A second instance of Apache can be installed as a dedicated Web server for hosting an organization's Web site or corporate intranet. You learn how to install and configure Apache Web Server to create a corporate Web site in “Installing and Configuring Web Services” later in this chapter.

## Tomcat Servlet Engine for NetWare

The Tomcat Servlet Engine, also developed by the Apache Group, is used to run Java-based Web applications (called **Java servlets**). It's used by several Net Services components, including Novell Portal Services (NPS) and NetWare Web Search Server. Although network administrators rarely need to configure or manage the Tomcat Servlet Engine, programmers developing Web-based applications often work with Tomcat because it runs on a wide variety of OSs.
