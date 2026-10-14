
## Managing Tomcat

The Tomcat servlet container provides a web interface for managing the applications and the Tomcat server itself. These functions require a user account login, which must be set in the configuration files.

- 1. Stop the Tomcat server using the command:
  
      `sudo /etc/init.d/tomcat6 stop`
  
- 2. Open the `/etc/tomcat6/tomcat-users.xml` file using the vim editor:
  
      `sudo vim /etc/tomcat6/tomcat-users.xml`
  
- 3. Create a manager and an admin role entry, then create a user entry for your username:
  
      ```xml
      <role rolename="admin"/>
      <role rolename="manager"/>
      <user username="rich" password="myword" roles="admin,manager"/>
      ```
  
      Be careful when adding the new lines. Scroll down below the `<tomcat-users>` tag to add new lines, but you must add them before the `<!--` comment tag line. If you place the lines after the `<!--` comment tag, Tomcat will assume they're commented out.
  
- 4. Save the file and exit. Use the ZZ command to save the text and exit the vim editor.
  
- 5. Restart Tomcat using the command:
  
      `sudo /etc/init.d/tomcat6 start`
  
- 6. Open a browser program on a client PC and access the manager page:
  
      `http://10.0.0.1:8080/manager/html`
  
- 7. Access the host admin page from the browser:
  
      `http://10.0.0.1:8080/host-manager/html`

The Manager web page, shown in Figure 21-11, allows you to manage existing Java servlet applications, as well as deploy new applications.

The Host Manager web page, shown in Figure 21-12, allows you to manage the virtual hosts created on the Tomcat 6 server (similar to the virtual hosts in the Apache web server).

For Java servlet applications, deploying a new application is a little more complicated than just copying a file, as you did with the JSP test application. Java servlet applications are deployed using a web archive (WAR) file. The WAR file contains compiled Java code files from the application. The manager web page allows you to upload a completed application WAR file to the server, then it places the WAR file in a new folder structure. Tomcat expands the WAR file automatically and modifies the configuration files to create the new application.

![](img/39e65eeb4f54001ede08c6114ae3cc6c_548_0.png)

Figure 21-11: The Tomcat 6 Manager web page.

![](img/39e65eeb4f54001ede08c6114ae3cc6c_548_1.png)

Figure 21-12: The Tomcat 6 Virtual Host Manager web page.

## Samba and Print Server

## Chapter 22

### Secrets in This Chapter

- What Is Samba?
- Samba in Ubuntu
- Configuring a Samba Server
- The CUPS Server

## What Is Samba?

Even though the Linux movement is gaining popularity, there’s no denying that the Microsoft Windows platform is still the major player in most computing environments. This doesn’t mean that you have to give up on your Ubuntu server if all of your workstations use Microsoft Windows. Your Ubuntu server is perfectly capable of playing nicely in your Windows environment, thanks to the Samba software package. This chapter discusses how to use Samba to allow the Microsoft Windows clients on your network to connect to shared folders and printers on your Ubuntu server. The chapter describes how Samba works in Ubuntu and demonstrates some simple configuration guides for creating shared folders and printers. The chapter also discusses the common UNIX printing system (CUPS), which allows you to share your Ubuntu system printers with other types of devices on your network.

The Samba software was created in 1992 by Andrew Tridgell to allow Linux systems to share resources with Microsoft Windows systems on a Windows network. The name Samba is somewhat of a play on the main protocol used in Microsoft networks, the server message block (SMB) protocol. Andrew fed the term SMB into a dictionary program to produce words that include those three letters. He decided on the name Samba.

Samba is now maintained by a team of volunteer developers, and it allows Linux systems to fully interact with all levels of the Microsoft Windows platform, both servers and workstations. Your Ubuntu server running Samba can interact with everything from Windows workstations using the old Windows 3.11 operating system to Windows 2008 servers. Samba also supports Microsoft’s common Internet file system (CIFS), which is Microsoft’s newer standard for PC network communication, based on the SMB protocol. This allows your Ubuntu server to access a shared folder on a Windows system as if it were mounted on the local Ubuntu server.

Samba implements the four basic CIFS services provided on a Windows network:

- File and print sharing
- Authentication and authorization
- Name resolution
- Service announcement (browsing)

By setting up the Samba software, you can use your Ubuntu server to share folders and printers from your Ubuntu server with any Windows client on the network, as well as with other Ubuntu servers and workstations running Samba. The Samba software also allows the Ubuntu workstation or server to connect to remote shared Windows folders and printers.

Besides managing shared folders and printers, Windows networking also manages hostnames. Windows networks use their own hostnames and their own hostname protocol, the NetBIOS name service (NBNS). The NBNS protocol allows clients and servers to connect to Windows servers using the name of the server rather than a network address. Windows networks use the Windows Internet name service (WINS) protocol to manage client and server names on the network.

Since the release of the Microsoft Windows NT server version, Microsoft networks also can contain specialized servers called domain controllers. A domain controller centralizes user account and share information for an entire Microsoft network. Once a server or
