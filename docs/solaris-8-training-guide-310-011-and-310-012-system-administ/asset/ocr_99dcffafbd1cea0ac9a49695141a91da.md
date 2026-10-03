NOTE
At times, I describe the boot server, the install server, and the configuration server as if they are three separate systems. The reality, however, is that most companies have one system that performs all three functions. I'll describe this in more detail in the “Install Server” section later in this chapter.

There are three main components to JumpStart:

+   - Boot and Client Identification Services. These services are provided by a networked boot server, and provide the information that a JumpStart client needs to boot using the network.
- Installation Services. These are provided by a networked install server, which provides an image of the Solaris Operating Environment the JumpStart client uses as its source of data to install.
- Configuration Services. These are provided by a networked configuration server, and provides information that a JumpStart client uses to partition disks and create file systems, add or remove Solaris packages, and perform other configuration tasks.

Each of these components is described in this chapter. If any of these three components is improperly configured, the JumpStart clients can:

+   - Fail to boot.
- Fail to find a Solaris Operating Environment to load.
- Ask questions interactively for configuration.
- Fail to partition disks, create file systems, and load the operating environment.

# PREPARING FOR A CUSTOM JUMPSTART INSTALLATION

The first step in preparing a custom JumpStart installation is to decide how you want the systems at your site to be installed. Here are some questions that need to be answered before you begin:

+   - Will the installation be an initial installation or an upgrade?
- What applications will the system support?
- Who will use the system?
- How much swap space is required?