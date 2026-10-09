
systems.

- **Multiple UNC Provider** (MUP) is a driver that determines which network to access when an application uses the Win32 I/O API to open remote files.

We conclude this section by describing Domain Name System, the heart of computer name resolution in Windows 2000.

## 6.3.1 Multiple Provider Router

The Win32 WNet functions allow applications (including the Windows Explorer My Network Places) to connect to network resources, such as file servers and printers, and to browse the contents of any type of remote file system. Because the WNet API can be called to work across different networks using different transport protocols, software must be present to send the request correctly over the network and to understand the results that the remote server returns. Figure 6.11 shows the redirector software responsible for these tasks.

A *provider* is software that establishes Windows 2000 as a client of a remote network server. The operations a WNet provider performs include making and breaking network connections, printing remotely, and transferring data. The built-in WNet provider includes a DLL, the WorkStation service, and the redirector. Other network vendors need to supply only a DLL and a redirector.

When an application calls a WNet routine, the call passes directly to the MPR DLL. MPR takes the call and determines which WNet provider recognizes the resource being accessed. Each provider DLL beneath MPR supplies a set of standard functions collectively called the *provider interface*. This interface allows MPR to determine which network the *application* is trying to access and to direct the request to the appropriate WNet provider software. The redirector’s provider is `\Winnt\System32\Nlanman.dll`, as directed by the ProviderPath value under the HKLM\SYSTEM\CurrentControlSet\Services\lanmanworkstation\NetworkProvider registry key.

When called by the *WNetAddConnection* API function to connect to a remote network resource, MPR checks the HKLM\SYSTEM\CurrentControlSet\Control\NetworkProvider\Order\ProviderOrder registry value to determine which network providers are loaded. It polls them one at a time in the order in which they’re listed in the registry until a redirector recognizes the resource or until all available providers have been polled. You can change the ProviderOrder by using the Advanced Settings dialog box, shown in Figure 6.12. (Only one provider is installed on the system from which the screen shot was taken.) This dialog box is accessible from the Advanced menu of the Network And Dial-Up Connections application. You can

![](img/e2283ffaea56e577ac05056b4bb738fc_163_0.png)

**Figure 6.11**
MPR components.

access the Network And Dial-Up Connections application by right-clicking the My Network Places icon on the desktop and selecting Properties from the pop-up menu or by selecting it from the Settings option from the Start menu.

The *WNetAddConnection* function can also assign a drive letter or device name to a remote resource. When called to do so, *WNetAddConnection* routes the call to the appropriate network provider. The provider, in turn, creates a symbolic-link object in the object manager namespace that maps the drive letter being defined to the redirector (that is, the remote FSD) for that network.

Figure 6.13 shows the `\\?` directory, where you can see several driver letters representing connections to remote file shares. The figure shows that the redirector creates a device object named `\\Device\\LanmanRedirector` and that the additional

![](img/e2283ffaea56e577ac05056b4bb738fc_164_0.png)

**Figure 6.12**
The provider order editor.

text included in the symbolic link's value indicates to the redirector which remote resource the drive letter corresponds to. When you open X:\Book\Chap13.doc, the redirector is passed the unparsed portion of the path that resolves through the

symbolic link, which is `\X:\dual\e\Book\Chap13.doc`. The redirector notes that the resource being accessed is located on the E share of server dual.

![](img/e2283ffaea56e577ac05056b4bb738fc_165_0.png)

**Figure 6.13**
Resolving a network resource name.

Like the built-in redirector, other redirectors create a device object in the object manager namespace when they are loaded into the system and initialized. Then, when the WNet or other API calls the object manager to open a resource on a different network, the object manager uses the device object as a jumping-off point into the remote file system. It calls an I/O manager parse method associated with the device object to locate the redirector FSD that can handle the request.

## 6.3.2 Multiple UNC Provider

The Multiple UNC Provider (MUP) is a networking component similar to MPR. It fields I/O requests destined for a file or a device that has a UNC name (names beginning with the characters `\\`, indicating that the resource exists on the network).

![](img/e2283ffaea56e577ac05056b4bb738fc_166_0.png)

**Figure 6.14**
Multiple UNC Provider (MUP).

MUP takes such requests and, like MPR, determines which local redirector recognizes the remote resource. Unlike MPR, however, MUP is a device driver (loaded at system boot time) that issues I/O requests to lower-layer drivers, in this case to redirectors, as shown in Figure 6.14.

The MUP driver is activated when an application first attempts to open a remote file or device by specifying a UNC name (instead of a redirected device letter, as described earlier). When the Win32 client-side DLL Kernel32.dll (which is the DLL that exports file/I-O-related APIs) receives such a request, the subsystem appends the UNC name to the string `\\UNC` and then calls the `NtCreateFile` system service to open the file. This object name is the name of a symbolic link that resolves to `\\Device\\Mup`, a device object that represents the MUP driver.

The MUP driver receives the request and sends an IRP asynchronously to each registered redirector, waiting for one of them to recognize the resource name and reply. When a redirector recognizes the name, it indicates how much of the name is

unique to it. For example, if the name is `\\WIN2KSERVER\\PUBLIC\incisedw2k\chap13.doc`, the redirector recognizes it and claims the string `\\WIN2KSERVER\\PUBLIC` as its own. The MUP driver caches this information and thereafter sends requests beginning with that string directly to the redirector, skipping the polling operation. The MUP driver’s cache has a timeout feature, so after a period of inactivity, a string’s association with a particular redirector expires. If more than one redirector claims a particular resource, the MUP driver uses the registry’s ProviderOrder value’s list of loaded redirectors to determine which redirector takes precedence.

## 6.3.3 Domain Name System

Domain Name System (DNS) is a standard by which Internet names (such as www.microsoft.com) are translated to their corresponding IP addresses. A network application that wants to resolve a DNS name to an IP address sends a DNS lookup request using the TCP/IP protocol to a DNS server. DNS servers implement a distributed database of name/IP address pairs that are used to perform translations, and each server maintains the translations for a particular zone. Describing the details of DNS is outside the scope of this book, but DNS is the foundation of naming in Windows 2000 and hence is the primary Windows 2000 name resolution protocol.

The Windows 2000 DNS server is implemented as a Win32 service (`\Winnt\System32\Dns.exe`) that is included in server versions of Windows 2000. Standard DNS server implementation relies on a text file as the translation database, but the Windows 2000 DNS server can be configured to store zone information in Active Directory.

## 6.4 Protocol Drivers

Networking API drivers must take API requests and translate them into low-level network protocol requests for transmission across the network. The API drivers rely on transport protocol drivers in kernel mode to do the actual translation. Separating APIs from underlying protocols gives the networking architecture the flexibility of letting each API use a number of different protocols. The protocol drivers that Windows 2000 includes are Data Link Control (DLC), NetBEUI, TCP/IP, and NWLink, although other protocols might be present as options, such as the AppleTalk protocol installed with Services For Macintosh on Windows 2000 servers.
