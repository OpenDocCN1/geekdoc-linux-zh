
# Chapter 1 • PLANNING YOUR ARCHITECTURE

A closer look at each of these classifications can help you understand the types of computer systems they include. With this information, you'll be prepared to classify systems within your own projects, and to project resource requirements for those classifications. Each type of machine has its own resource requirements, including:

- Physical size of the hardware
- Operating system
- Memory
- Storage capacity
- Processor requirements
- Graphics capabilities

## Desktop Workstations

A desktop workstation is intended for console by people of varying computer literacy, and it can be the simplest of systems. Workstations can be optimized for particular applications (such as graphic design, mathematics, or statistical programs) or for general office tasks such as word processing, spreadsheets, email, scheduling, group collaboration, and so on.

Workstations require keyboards, video cards, and monitors, and they typically have a modest amount of physical memory for applications and local disk storage. Most workstations use network file servers for the majority of their data and application storage (you learn more about file servers in the "File Server" section, later in this chapter).

## Classifying Workstations

Desktop workstations are used for a variety of tasks from word processing to video rendering applications. Although a workstation used for word processing doesn't need much memory or a fast CPU, the video rendering workstation requires a significant amount of memory and processing power, in addition to a high-end graphics card. Classifying your workstations based on the applications users will run from them helps you identify these resource requirements up front.

## Interactive Login Servers

A login server is a system to which many users can connect remotely in order to access various interactive applications, usually Unix shells. Login servers may require a large amount of memory to accommodate many simultaneous user applications. A login server's operating system needs to be finely tuned to maintain a reasonable response time for interactive applications.

## University of Michigan Login Servers

A pool of login servers at the University of Michigan is used by the university community for general-purpose Unix applications. The majority of users run pine, a popular Unix mail program, to check their email, while others use newsletters, compilers, and text editors for various purposes, types of applications and uses found in any classic real-world example of an interactive server. The administrators of these systems constantly monitor them for excessive load, tune them for good interactive response, and keep the hundreds of installed software packages up to date.

## Application Servers

Application servers host the applications that are visible to your customers and outside the organization, and they are the front ends for your services. Examples of application servers include Web servers, FTP servers, and servers for any application available for use by your customers. This category of servers is generic, as the resource requirements of the system depend heavily on the needs of the application running on that system; in general, however, systems in this category need to be running at all times and be able to handle the volume of requests you expect to receive.

## Database Servers

Database servers run the software that manages your databases. They are the back end of your product, typically utilized by application servers, and not visible to the public. Databases typically require large amounts of memory and enormous amounts of disk space. Database servers must have minimal downtime; your data is unavailable if your database server is down.

Data integrity is also of great importance on a database server. A database is not very useful if it contains bad data. Databases can also require a significant backup infrastructure, especially if you're running several databases on multiple servers.

## Redundancy for Critical Servers

Critical database servers should also include some form of redundancy so that if one server fails, another one can take over the entire site doesn't go down. Chapter 10, "Providing High Availability in Your Unix System," discusses this topic in more detail.

## Computer Servers

One frequently overlooked use of computers is computing. Mathematics and statistics programs, as well as digital rendering applications and systems used in projects such as SETI (Search for Extra-Terrestrial Intelligence) requires enormous amounts of computing power to achieve their full potential. Computer servers need large amounts of memory, large amounts of local disk space for temporary storage, and—most important—uptimes measured in months, not days. Calculations can take weeks to complete, and nobody wants to start over because of a system failure.

![](img/894492738e879267320b8d6f9a044180_32_0.png)

## Real-World Example: Failing Compute Servers

A bug in the operating system of one of the compute servers at a university caused it to reboot every week or two. Many of its users complained that these reboots interrupted their long-running computations, some which ran for days or weeks at a time, and forced them to be restarted. The problem was delaying university research, prompting the system administrators to escalate the problem with the operating system vendor. The vendor issued a patch several weeks later, which solved the problem. In the case of compute servers, 24/7 availability is not just something to strive for—it’s a requirement.

## File Servers

In today's networked environments, storing common files and applications on a central server that's accessible by various clients is both convenient and cost effective. These central servers, called file servers, are critical to any infrastructure. Because these systems serve the programs and data used by every person and every system on the network, they need to be available 24 hours a day, seven days a week. File servers require a large amount of disk space for file storage and high-speed network connections to serve large amounts of data to clients. They also need to be backed up on a regular basis.

## Administrative Servers

Administrative servers house the applications that provide your entire infrastructure relies on basic network functionality. These services provide DNS, email, log collection, time synchronization, and authentication servers. Resource requirements for administrative servers vary, especially with mail servers; but because these servers provide basic functionality for your network, they must have a minimum amount of downtime.

Classifying individual systems is an easy way to begin specifying the hardware you need for your project. Systems with similar classifications require similar amounts of resources like memory, CPU, and storage, which means you can quickly identify the minimum requirements for any type of system your projects call for.

## Collecting Specifications

"We need a database server."

"Our mail server is failing. Get a better one."

"We're hiring 50 new employees next month. Let’s buy more disks for our increased needs. We should probably back up that too, right?"

You may have heard similar statements from your own management at one time or another—and you’ll hear them again. Clients and management often make requests for more or better systems and services, making those requests and suggestions is their job.

Of course, not all requests are reasonable. You might find, for example, that fixing the problem with that pesky mail server is more cost-effective than purchasing a new one. You discover that the mail server's network card is dropping packets, and you know that your support contract with the vendor allows you to request a replacement free. If you purchased a new server, as management requested, the company would have spent thousands of dollars unnecessarily.

As this example demonstrates, companies get the most effective use of their systems—system administrators—leaving the technical decisions with technical people. As system administrator, your job becomes that of gathering information about what users want the system to do or provide; then, you can determine the best way to meet the project's goals and requirements. To do your job properly, you first need to help management express your business goals as accurately as possible; then, you must be capable of constructing a detailed technical plan for achieving these goals.

## Ask for Goals, Not Methods

Force your management to communicate their business goals, rather than their ideas for technical solutions. Devising and implementing those solutions is your job.

## Translating Business Goals into Technical Solutions

Business goals should dictate what the end result of a project should be, and how the new system will aid the company's business. Your job is to translate these business goals into technical solutions that will produce the results management is looking for.

To better understand that process, consider some typical business goals and how they translate into technical solutions for achieving those goals. For example, this business goal:

- Recruit 5,000 additional users for our email service.

might translate into this technical solution:

- 1. Verify we can back up an additional 50GB of mail (assuming an average of 10MB per email user).
- 2. Order and install 50GB of disk space on our mail server.
- 3. Add the new space to the mail pool file system.

Other business goals are not easily resolved, however. This business goal:

Our Web site should be able to support one million hits per day.

might translate into:
