
**datagram** A self-contained, independent entity of data carrying sufficient information to be routed from the source to the destination computer without reliance on earlier exchanges between this source and destination computer and the transporting network. *UDP* (page 1278) uses datagrams; *IP* (page 1255) uses *packets* (page 1265). Packets are indivisible at the network layer; datagrams are not. See also *frame* (page 1251).

**dataless** A computer, usually a workstation, that uses a local disk to boot a copy of the operating system and access system files but does not use a local disk to store user files.

**dbm** A standard, simple database manager. Implemented as **gdbm** (GNU database manager), it uses hashes to speed searching. The most common versions of the **dbm** database are **dbm**, **ndbm**, and **gdbm**.

**DDoS attack** Distributed denial of service attack. *A DoS attack* (page 1248) from many systems that do not belong to the perpetrator of the attack.

**debug** To correct a program by removing its bugs (that is, errors).

**default** Something that is selected without being explicitly specified. For example, when used without an argument, `ls` displays a list of the files in the working directory by default.

**delta** A set of changes made to a file that has been encoded by the Source Code Control System (SCCS).

**denial of service** See *DoS attack* on page 1248.

**dereference** To access the thing to which a pointer points, that is, to follow the pointer. At first sight the word *dereference* might be thought to mean “to cause to stop referring,” but its meaning is well established in jargon.

When speaking of symbolic links, *dereference* means to follow the link rather than working with the reference to the link. For example, the `-L` or `--dereference` option causes `ls` to list the entry that a symbolic link points to rather than the symbolic link (the reference) itself.

**desktop** A collection of windows, toolbars, icons, and buttons, some or all of which appear on your display. A desktop comprises one or more *workspaces* (page 1281).

**desktop manager** An icon- and menu-based user interface to system services that allows you to run applications and use the filesystem without using the system’s command-line interface.

**detached process** See *background process* on page 1238.

**device** A disk drive, printer, terminal, plotter, or other input/output unit that can be attached to the computer. Short for *peripheral device*.

**device driver** Part of the Linux kernel that controls a device, such as a terminal, disk drive, or printer.

**device file** A file that represents a device. Also *special file*.

**device name** The pathname of a device file. All Linux systems have two kinds of device files: block device files and character device files. Linux also has FIFOs (named pipes) and sockets. Device files are traditionally located in the /dev directory.

**device number** See *major device number* (page 1259) and *minor device number* (page 1261).

**DHCP** Dynamic Host Configuration Protocol. A protocol that dynamically allocates IP addresses to computers on a LAN.

**dialog box** In a GUI, a special window, usually without a titlebar, that displays information. Some dialog boxes accept a response from the user.

**directory** Short for directory file. A file that contains a list of other files.

**directory hierarchy** A directory, called the root of the directory hierarchy, and all the ordinary files below it (its children).

**directory service** A structured repository of information on people and resources within an organization, facilitating management and communication.

**disk partition** See *partition* on page 1265.

**diskless** A computer, usually a workstation, that has no disk and must contact another computer (a server) to boot a copy of the operating system and access the necessary system files.

**distributed computing** A style of computing in which tasks or services are performed by a network of cooperating systems, some of which might be specialized.

**DMZ** Demilitarized zone. A host or small network that is a neutral zone between a LAN and the Internet. It can serve Web pages and other data to the Internet and allow local systems access to the Internet while preventing LAN access to unauthorized Internet users. Even if a DMZ is compromised, it holds no data that is private and none that cannot be easily reproduced.

**DNS** Domain Name Service. A distributed service that manages the correspondence of full hostnames (those that include a domain name) to IP addresses and other system characteristics.

**DNS domain name** See *domain name*.

**document object model** See *DOM*.

**DOM** Document Object Model. A platform-/language-independent interface that enables a program to update the content, structure, and style of a document dynamically. The changes can then be made part of the displayed document. Go to www.w3.org/DOM for more information.

**domain name** A name associated with an organization, or part of an organization, to help identify systems uniquely. Technically, the part of the FQDN (page 1250) to the right of the leftmost period. Domain names are assigned hierarchically. The domain berkeley.edu refers to the University of California at Berkeley; for example, it is part of the top-level edu (education) domain. Also *DNS domain name*. Different than *NIS domain name* (page 1263).

| Term | Description |
|---|---|
| **Domain Name Service** | See *DNS*. |
| **door** | An evolving filesystem-based RPC (page 1271) mechanism. |
| **DoS attack** | Denial of service attack. An attack that attempts to make the target host or network unusable by flooding it with spurious traffic. |
| **DPMS** | Display Power Management Signaling. A standard that can extend the life of CRT monitors and conserve energy. DPMS supports four modes for a monitor: Normal, Standby (power supply on, monitor ready to come to display images almost instantly), Suspend (power supply off, monitor takes up to ten seconds to display an image), and Off. |
| **drag** | The motion part of drag-and-drop. |
| **drag-and-drop** | To move an object from one position or application to another within a GUI. To drag an object, the user clicks a mouse button (typically the left one) while the mouse pointer hovers (page 1253) over the object. Then, without releasing the mouse button, the user drags the object, which stays attached to the mouse pointer, to a different location. The user can then drop the object at the new location by releasing the mouse button. |
| **drop-down list** | A widget (page 1281) that displays a static list for a user to choose from. When the list is not active, it appears as text in a box, displaying the single selected entry. When a user clicks the box, a list appears; the user can move the mouse cursor to select an entry from the list. Both operating systems use a list box (page 1258). |
| **druidd** | In role-playing games, a character that represents a magical user. Fedora/RHSEL uses the term *druid* at the ends of names of programs that guide you through a task-driven chain of steps. Other operating systems call these types of programs *wizards*. |
| **DSA** | Digital Signature Algorithm. A public key cipher used to generate digital signatures. |
| **DSL** | Digital Subscriber Line/Loop. Provides high-speed digital communication over a specialized, conditioned telephone line. See also *xDSL* (page 1282). |
| **Dynamic Host Configuration Protocol** | See *DHCP* on page 1247. |
| **editor** | A utility, such as *vim* or *emacs*, that creates and modifies text files. |
| **EEPROM** | Electrically erasable, programmable, read-only memory. A PROM (page 1267) that can be written to. |
| **effective UID** | The UID (user ID) that a process appears to have; usually the same as the real UID (page 1269). For example, while you are running a setuid program, the effective UID of the process running the program is that of the owner of the program, frequently *root*, while the real UID remains your UID. |
| **element** | One thing; usually a basic part of a group of things. An element of a numeric array is one of the numbers stored in the array. |
| **emoticon** | See *smiley* on page 1273. |
