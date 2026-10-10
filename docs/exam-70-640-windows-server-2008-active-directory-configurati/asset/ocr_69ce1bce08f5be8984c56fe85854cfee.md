**clock skew** The time difference between any client or member server and the domain controllers in a domain.

**Comma-Separated Value Directory Exchange (CSVDE)** The command-line utility used to import or export Active Directory information from a comma-separated value (.csv) file.

**Comma-Separated Values (CSV)** Format that contains a comma between each value. The CSV format can be used to import and export information from other third-party applications.

**Common Information Management Object Model (CIMOM)** A database used through Windows Management Instrumentation that contains information gathered when a computer starts and becomes part of the network. This information includes hardware, Group Policy Software Installation settings, Internet Explorer Maintenance settings, scripts, Folder Redirection settings, and security settings.

**compressed** To reduce the size of transmitted data to decrease the use of network bandwidth.

**Computer Configuration** A Group Policy setting that enables administrators to customize the configuration of a user’s desktop, environment, and security settings. Enforced policies are based on the computer used.

**conditional forwarders** A server that will forward queries selectively based on the domain specified in the name resolution request.

**Configuration NC** The configuration partition contains information regarding the physical topology of the network, as well as other configuration data that must be replicated throughout the forest.

**connection objects** The link, created by the Knowledge Consistency Checker, between domain controllers that replicate with one another in a site.

**container object** An object, such as a domain or an Organizational Unit, that is used to organize other objects. Also known as a *leaf object*.

**convergence** The amount of time required for replication so that all domain controllers in the environment contain the most up-to-date information.

**copy backup** A backup type that retains the Application log files on the local server. This backup logy should be implemented if a third-party backup tool is used in addition to Windows Server Backup.

**cost** Value assigned to a site link object to define the path that replication will take. If more than one path can be used to replicate information, cost assignments will determine which path is chosen first. A lower-numbered cost value will be chosen over a higher-numbered cost value.

**critical volumes** Volumes that should be backed up.

**cross-forest trust** Trust type that allows resources to be shared between Active Directory forests.

**d**

**dcdiag** A command-line tool used for monitoring Active Directory.

**dcpromo** The Active Directory Installation Wizard.

**Default Domain Controller Policy** A policy linked to the Domain Controllers OU; its settings affect all domain controllers in the domain.

**Default Domain Policy** A policy linked to the domain; its settings affect all users and computers in the domain.

**defragmentation** The process of taking fragmented database pieces and rearranging them contiguously to make the database more efficient.

**delegation** Administration of an Organizational Unit is tasked to a departmental supervisor or manager, thus allowing that person to manage day-to-day resource access as well as more mundane tasks, such as resetting passwords.

**Delegation of Control Wizard** A simple interface used to delegate permissions for domains, Organizational Units, and containers.

**dictionary attack** Automated pass-word-cracking tools that try every possible combination of characters until the correct sequence of characters is finally discovered.

**digital certificate** A digital document that contains identifying information about a particular user, computer, service, and so on. The digital certificate contains the certificate holder’s name and public key, the digital signature of the Certificate Authority that issued the certificate, as well as the certificate’s expiration date. Also known as a *certificate*.

**digital signature** This electronic signature (created by a mathematical equation) proves the identity of the entity which has signed a particular document.

**directory service** Allows businesses to define, manage, access, and secure network resources, including files, printers, people, and applications.

**Directory Services Restore Mode** A special startup mode used to run an offline defragmentation.

**disallowed** Strategy for enforcing restrictions that prevents all applications from running except those that are specifically allowed.

**disk quotas** A setting that limits the amount of space available on the server for user data.

**distinguished name (DN)** The full name of an object that includes all hierarchical containers leading up to the root domain. The distinguished name begins with the object’s common name and appends each succeeding parent container object, reflecting the object’s location in the Active Directory structure.

**distribution group** Non-security-related groups created for the distribution of information to one or more persons.

**distribution share** The shared folder that is a network location from which users can download software. Also known as the *software distribution point*.

**DNS domain** An administrative entity that consists of a group of hosts, usually a combination of computers, routers, printers, and other TCP/IP-enabled devices.

**DNS namespace** Consists of a hierarchy of domains. Each domain has DNS name servers that are responsible for supplying information about the hosts in that domain.

**domain** A grouping of objects in Active Directory that can be managed together. A domain can function as a security boundary for access to resources, such as computers, printers, servers, applications, and file systems.

**domain account** The accounts used to access Active Directory or network-based resources, such as shared folders or printers.

**domain controller (DC)** A server that stores the Active Directory database and authenticates users with the network during logon.

**domain GPO** A type of Group Policy Object associated with a domain.

**domain local group** A group used to assign permissions to resources that reside only in the same domain as the domain local group. They can contain user accounts, computer accounts, global groups, and universal groups from any domain, in addition to other domain local groups from the same domain.