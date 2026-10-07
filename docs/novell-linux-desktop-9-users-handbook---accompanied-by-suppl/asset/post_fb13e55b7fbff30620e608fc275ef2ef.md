
# CHAPTER 1: Start Here

So as we discuss the ins and outs of Novell Linux Desktop in this book

# NOTE

For more information on where OpenOffice.org came from and where it is going as an application suite, check out http://www.openoffice.org.

# Novell Linux Desktop Applications and Tools

Writer is a powerful document processor and is part of the OpenOffice.org productivity suite

![](img/6e85ebc4ce06a64c82109523b60183ba_24_0.png)

# Mozilla Firefox

Whether you use the Web for business, research, or entertainment, it's important to have a web browser that minimizes the dangers of adware, pop-ups, and spyware. Your web browser also makes it easy for you to find the websites you are looking for and to save your web addresses for later reference. Mozilla Firefox fulfils all these requirements and more.

Mozilla Firefox is cross-platform (available for more than one operating system platform including Linux and Microsoft Windows) GNU software and provides unique features such as tabbed web browsing and a built-in pop-up blocker.

We will take a closer look at Mozilla Firefox in Chapter 8, which includes information on creating and managing bookmarks, blocking pop-ups, and using tabbed browsing.

# NOTE

For general information and various reviews of Mozilla Firefox check out http://www.mozilla.org/products/firefox/

# CHAPTER 1: Start Here

The Novell Firefox web browser window.

![](img/6e85ebc4ce06a64c82109523b60183ba_25_0.png)

# Novell Evolution

All computer users, particularly those who use the PC extensively as a business tool, strive to stay organized and maintain a list of appointments, contacts, and emails. Novell Evolution is a groupware product that pulls together important business tools into one software package. Novell Evolution allows you to manage your email, calendar, contacts, and tasks. It also provides connectivity with network groupware servers as as Novell GroupWise and Microsoft Exchange. Chapter 14, “Managing Email and Contacts with Novell Evolution,” and Chapter 15, “Staying Organized with Novell Evolution,” provide more detailed information on how to use Novell Evolution.

# KEY TERM

Groupware—Client communication software that allows collaboration with other users and is designed to connect to a communication server product.

# Novell Linux Desktop Applications and Tools

Keep track of your appointments with Novell Evolution's Calendar.

![](img/6e85ebc4ce06a64c82109523b60183ba_26_0.png)

# Other NLD Tools

NLD also provides a number of other tools—for example, a calculator, dictionary, and file manager (the Nautilus File Manager, covered in Chapter 6, “Managing Files”). Each of these tools can be opened via the Accessories submenu on the NLD Programs menu.

# NOTE

NLD includes a lot of other software. You can play and burn CDs, watch a DVD movie (if your PC has a DVD drive), and even play a number of preinstalled games.

# CHAPTER 1: Start Here

Tools such as file manager, directory, and calculator are readily available from the Accessories submenu.

![](img/6e85ebc4ce06a64c82109523b60183ba_27_0.png)

# Novell Linux Desktop Installation Considerations

Before you can take advantage of all the possibilities that NLD provides, you need to install the operating system on your computer. In most business settings your computer support personnel have probably already taken care of the installation. In case you are installing NLD yourself, this section provides some general information on the installation process.

NLD can be installed from CDs or DVDs, and the installation process for NLD is straightforward. The process is handled by YaST, an installation and configuration utility that walks you step-by-step through the install process (it is actually an automated version of YaST called autoYaST that handles the NLD installation).

# NOTE

YaST (Yet Another Setup Tool) also serves as the configuration tool used to change administrative settings related to hardware and software. YaST requires the use of the root account. YaST is actually provided by the SUSE Linux core that drives the NLD OS.

# Novell Linux Desktop Installation Considerations

YaST allows you to select settings such as the language to be used, the default desktop (GNOME or KDE), and the time zone. In terms of identifying hardware components on the PC, YaST can actually recognize hardware configurations during the installation process, which means that much of the work you do is to accept YaST-determined settings and move on to the next step in the process.

Let's take a look at the hardware requirements for the installation of NLD. We can then take a look at how Linux partitions are used to partition your computer's hard drive. We can then look at some of the highlights related to the actual installation process.

# Hardware Requirements

Novell provides both minimum and recommended hardware configurations for the installation of NLD. These system requirements follow:

- Processor—Intel Pentium II or compatible running at 266 MHz minimum, with a recommended processor of Intel Pentium III or compatible running at 500 MHz.
- Memory (RAM)—256MB minimum and 500MB or more suggested.
- Video display—A video card that can display 800X600 pixels is the minimum, and a display that provides 1024X768 pixels is suggested.
- Hard drive space—a minimum of 800MB is suggested, and 2GB or more is recommended.

It is safe to say that in terms of hardware configurations more is always better. The higher the processor speed, the greater the memory, and the more fixed disk space available, the better NLD will run upon your PC.

# Understanding Linux Partitions

During the NLD installation process your hard drive (we assume a single hard drive on the computer) is partitioned. A partition is actually a way to logically divide the disk space into pieces recognizable by the operating system. In Windows, these partitions are assigned drive letters, but not in Linux.

AutoYaST takes a look at your hard drive and creates two partitions during the installation: a swap partition and a root partition. These partitions would be specified as /dev/sda1 and /dev/sda2, respectively, on an IDE hard drive (/dev/sda1 and /dev/sda2 on a computer using SCSI drives). You need both of these partitions for the system to function. The swap partition is used by the system to hold excess process and information that it can't currently copy into

# CHAPTER 1: Start Here

the memory. So, the swap drive is basically used to swap information in and out of the computer's memory as you use the computer. A root partition is also created and used as the main drive for the system. This drive is required for the system to boot.

Other partitions can be created during the installation. But the process requires a working knowledge of partitioning. Because data directories can be used for different users and other purposes, it may make sense to allow YaST to perform the partitioning for you.

# NOTE

If you attempt to install a dual-boot system that runs NLD and another operating system (such as an existing Windows installation), you might need to create your own partitions during the NLD installation. Typically, YaST looks at your hard drive and attempts to resize the existing partition to create space for the swap and root partitions.

![](img/6e85ebc4ce06a64c82109523b60183ba_29_0.png)

# Novell Linux Desktop Installation Considerations

We will take a closer look at directories and file systems in Chapter 6, which provides further insight into the naming conventions of Linux partitions and how to navigate them.

# Other Tips on the NLD Installation Process

Before we end our discussion of the NLD installation and then move on to actually exploring NLD and the software that provides, a few other items should be discussed. First, in terms of the overall installation process, it is probably best to allow YaST to do its job and configure the system for you. This means that you click Accept more than not.

When you first boot the system for the installation (your NLD CD or DVD should be in the appropriate drive), the first installation screen that appears can be a little confusing. Press the down arrow key on the keyboard to select Installation. You can then press Enter and begin the installation process.

![](img/6e85ebc4ce06a64c82109523b60183ba_30_0.png)

At least two accounts are created during the NLD installation: root and a user account. As already mentioned, the root account is the administrative account for the NLD system. The password created for root should be between five and eight characters and consist of alphanumeric (both letters and numbers) characters. You can also vary the case of the characters in the password, but you have to be able to repeat the password exactly as it was created (including case). This makes a strong password, meaning that it is more difficult to guess.
