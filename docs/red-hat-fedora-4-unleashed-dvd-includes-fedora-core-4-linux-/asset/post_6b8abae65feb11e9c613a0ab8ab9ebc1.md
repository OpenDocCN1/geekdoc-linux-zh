
## System Considerations

deployment, scaling, maintenance, resource requirements, and support of legacy hardware.

You should know what you are going to do with Linux before you install it. In other words, what is the objective of your migration? If Fedora will be used as a replacement platform for network services, what services will be replaced? What types of applications will need support? If Fedora is deployed as a new desktop for administrative users?

Some research might be required beforehand, and you might want to compare software performance of desired services against your existing infrastructure, using a time-lined prototype install or deployment. Such testing is not a special requirement unique to a Linux migration, but a normal part of a careful consideration process before investing time and effort—which will represent your major costs because Linux and its major software is free.

Fedora is a perfect solution for many computing needs. However, choosing an operating system platform mandates consideration of a number of issues. Some of these issues are listed in Table 2.1. For example, how you choose to use Fedora will affect your choice of computer hardware, might affect your network configuration, and could dictate software policy issues (such as access, security, and allowable protocols).

Linux-based operating systems can be used to provide many different services. For example, one server might be boot management for a thin-client network in which workstations boot to a desktop by drawing a kernel and remotely mounted file systems over a network. This mechanism is not supported out of the box, so some effort can be expended if such a system is required. Other services more easily implemented (literally in an hour or less) could be centralized server environments for file serving, web hosting for a company intranet, or bridging of networks and routing services.

Linux supports nearly every network protocol, which enables it to be used to good effect even in mixed operating system environments. The security features of the Linux kernel and companion security software also make Linux a good choice when security is a top priority. Although no operating system or software package is perfect, the benefit of open source of the kernel and other software for Linux allows peer review of pertinent code and rapid implementation of any necessary fixes. Even with the secure features of Linux, some effort will have to be made in designing and implementing gateways, firewalls, or secure network routers.

Fedora can serve as a development platform for applications, e-commerce sites, new operating systems, foreign hardware systems, or design of new network devices using Linux as an embedded operating system. Setting up workstations, required servers, source code control systems, and industrial security will require additional effort.

Hardware compatibility can be an issue to consider when setting up a Linux server or building a Linux-based network. Fortunately, enlightened computer equipment manufacturers are beginning to realize that Linux-based operating systems (like other open-source operating systems such as BSD) are increasingly popular, support open standards, and offer technologies that can help rapid introduction of products into the market (through third-party developer communities).

Fedora can help ease system administration issues during migration. The latest suite of Fedora’s configuration utilities provide intuitive and easy to use graphical interfaces for system administration of many common services, such as networking, printing, and Windows-based file sharing. Fedora can also be used to support legacy application environment, such as DOS, if required.

## User Considerations

Humans are creatures of habit. So it can be hard to transition a workforce, customer base, or other community to a new environment. The Fedora desktop, however, provides a friendly and familiar interface with menus and icons that new users can readily learn and put to work.

Part of the migration process can involve addressing user concerns, especially if Linux will take over the desktop. Fedora can be deployed in stages to make the migration process a bit easier, but the issue of user training will need to be addressed early on. This is especially true if users will be required to develop new skills or be aware of any caveats when using Linux (such as deleting all files in one’s home directory). Although Fedora can be configured to provide a “turn-key” desktop in which only several graphical applications (such as a web browser, organizer, or word processor) can be used, some users will want and need to learn more about Linux.

You can turn to formal Linux training from commercial vendors. System administrators can get training directly from Red Hat (go to http://www.redhat.com/training). For other issues concerning Linux in larger computing environments, browse to Linas Vepstas’s Linux Enterprise Computing pages at http://linas.org/linux/.

## A Predeployment Planning Checklist

Table 2.1 provides a minimal checklist you can use to help plan a deployment.

| Consideration | Description |
| :-- | :-- |
| Applicability | How is Fedora going to be used? |
| Boot Management | Will remote booting be required? |
| Connectivity | Will the system be an intranet? Bandwidth requirements? Wireless? Mobile? |
| Context | How does this install fit in with academic, business, or corporate needs? |
| Consensus | Are managers and potential users on board with the project? |
| Comparison | Is this install part of platform comparison or benchmarking? |
| Development Platform | Will development tools be used? |
| Embedded Device | Is it an embedded device project? |
| Hardware | Are there any special hardware or device interfacing requirements? |
| Finance | How much is in the budget? Will cost comparison be required? |
| Marketing | Will a product or service be offered as a result? |
| Networking | What type of networking will be required? |
| Objective | Is there a specific objective of the install? |
| Power Management | Any special power or energy requirements? |
| Prototype Project | Is this a prototype or test install? |
| Public Relations | Does the public need to know? |
| Quality of Service | Is high availability or data integrity an issue? |
| Roadmap | What other steps might precede or follow the install? |
| Reporting | Are follow-up reports required? |
| Security | What level or type of security will be required? |
| Server | Is this a server installation? |
| Site Considerations | Does the location provide needed temperature and security, or does it even matter? |
| Software | Are any special device drivers needed for success? |
| Storage | Are there size or integrity needs? Has a backup plan been devised? |
| Timeline | Are there time constraints or deadlines to the install? |
| Training | Will special training be required for users or administrators? |
| Users | How many and what type of users are expected? |
| Workstation | Is this a workstation or personal desktop install? Is the workstation portable? |

Do not forget to address follow-up issues on your migration roadmap. You should pay attention to how satisfied or how well new users, especially those new to Linux, are adapting if a new desktop is used. However, if Fedora is deployed in a mixed environment, many users might not even know (or need to know) that Linux is being used!

## Planning the Installation

There are many factors in favor of using Fedora Core as a computing solution. The current distribution can fill many different roles on various tiers and hardware platforms because its preconfigured installation scripts are a tailored fit for development, workstation, e-commerce, server, and mobile platforms—only the required software will be installed. Addressing concerns beforehand can help quell any worries or fears felt by new users. Some key factors for a successful installation include:

- **Preparation**—Thoroughly discuss the migration or deployment, along with benefits, such as greater stability and availability of service.
- **Preconfiguration**—If possible, give users a voice in software choices or categories and poll for comments regarding concerns.
- **Correct installation**—Ensure that the installed systems are working properly, including access permissions, password systems, or other user-related issues and interaction with the deployment.
