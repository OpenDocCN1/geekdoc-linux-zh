
## Selling Your Used Computer

One way to upgrade your mobile life is to sell your old notebook before buying a new one. Most smart sellers use the local classifieds and price their notebook according to its proper market value (at least 50 percent less after its first birthday). You can also try to sell on the Internet through various Usenet newsgroups or an online auction house, but don’t be disappointed if you are consistently lowballed on the price. You shouldn’t expect to even recoup the expense of costly add-ons, such as RAM or a larger hard drive.

U.S. small business owners should note that if the full price of the notebook is depreciated in its first year of use, you must wait three years before disposing of the laptop.

## Buying a Used Computer

There are ways to get your hands on a (relatively) new notebook. First, you can scour the classifieds and hope to find a new model of the desired notebook. An alternative is to buy a refurbished notebook. Computer makers such as IBM, Dell, and Sony routinely offer refurbished units at considerable savings. The iBook used as an example during the writing of this book was a refurb, and much of this book was developed using Linux on a refurbished ThinkPad i1720. By dealing with a reputable company, you can be assured of getting some warranty coverage from the seller.

Some local computer resellers might sell used notebooks. In fact, I have an AST Ascentia A61+ laptop purchased locally in 1997 that is still trucking along, running Linux 24 hours a day, 7 days a week.

I do not recommend buying a computer from any FS: (For Sale) posting in any Usenet newsgroup. I also recommend not buying through an online auction service (such as www.ebay.com) unless you use an escrow service and get the seller to pay the escrow charges. This is a much safer way of buying a notebook, and it sure beats sending money to someone you've never met and not getting a notebook in return. There are many tales of woe from online buyers who failed to exercise caution and use common sense in pursuing online purchases.

Whenever possible, pay by credit card, not by check, money order, or cash. You'll have a much better chance of getting consumer satisfaction by threatening to dispute any charge for faulty merchandise.

But you should also understand that used notebooks (indeed, any used computer equipment) are usually sold "as is." Cavet emptor!

# Living with Your Choice: Trade-Offs

If you have to make do with what you have, so be it. But you'll be much more ready for a Linux installation if you learn as much as you can about your computer. (See Chapter 2, "Taking Inventory," for details about various components.) For example, you should know the following:

- How to turn your notebook off and on
- How to control the speakers or sound system
- Where the PC card slot or slots are located
- The type of pointing device used (most likely PS/2 for Intel computers and definitely a one-button ADB desktop mouse for Apple iBook users)
- Any keyboard controls for turning the LCD screen off or on
- Where the microphone is located
- How to insert, remove, or recharge your notebook's battery
- Where the ports—such as serial, IrDA, line-in, line-out, headphone, USB, monitor, and PS/2—are located

In other words, read your computer's manual before installing Linux! If you do not have a manual, you can try downloading one from your computer's manufacturer. Some companies, such as IBM, not only maintain user manuals for older notebooks, but they also offer technical repair manuals containing detailed disassembly information for free.

If you have an old notebook from a manufacturer that has gone out of business, you might find a company providing repair services or other information by searching the Web. Otherwise, you'll have to wing it. In general, if the notebook is Intel-based, it's at least a 386 equivalent, and it can run DOS, it can run Linux.

If you find that Linux does not fully support your laptop, take heart! If the laptop is a new model and becomes popular, it will be supported—but it might take some time! Major manufacturers are now wising up to the fact that Linux is not just a “flash in the pan” operating system, but is here to stay. Users are demanding support and are requiring compatibility with Linux.

## Resource Information

- http://www1.pcworld.com/current_issue/article/0,1212,10226+1+0,00.html
  “Who Made Your Notebook? Don't Believe the Label,” *PC World* Magazine, May 1999
- http://www.fringeweb.com/laptops.html
  A place to find out who makes which laptop.
- http://www.cs.utexas.edu/users/kharker/linux-laptop/
  Kenneth Harker's *definitive* Web site provides a great guide to using Linux on a laptop. Numerous specific laptop model links to sites detailing the experiences of those who have gone before you.
- http://www.xfrec86.org
  The place to read about the free X Window System distribution for Linux and other operating systems. A good place to start researching graphics chipset compatibility.
- http://www.opensound.com/osswh.html
  Lists sound cards supported by commercial Linux kernel sound modules from 4Front Technologies.
- http://www.alsa-project.org
  A list of sound cards supported by these alternative Linux drivers.
- http://home.att.net/–tpbrown/01/PC_FAQ1.html
  Portable computing FAQ.
- http://www.dell.com/us/en/dhs/topics/linux_peripherals.htm
  A list of supported peripherals and components of Inspiron and Latitude notebooks.
- http://www.tuxtops.com
  A new Linux notebook reseller.
- http://www.suse.com
  Information about SuSE Linux on DVD.
- http://www.linmodems.org
  An optimistic Web site with links to possible solutions for using a Windows modem with Linux.
- http://www.aslab.com
  A Linux notebook reseller.

# Chapter 2: Taking Inventory

- Type of CPU
- Your Notebook's Display
- XFi Configuration Utilities
- Your Notebook's Sound System
- Your Notebook's Keyboard
- Your Notebook's Pointer
- Your Notebook's Memory
- Your Notebook's Hard Drive
- Your Notebook's CD-ROM
- The Parallel Port
- The PCMCIA Port
- Serial Ports
- Internal Modems
- External Monitor Port
- Infrared Port
- Universal Serial Bus
- IEEE 1394 (FireWire)
- Your Notebook's Battery
- Docking Stations
- Resource Information

**O**ne of the best ways to ensure success when installing and configuring Linux is to understand the hardware elements of your notebook. Mobile Linux users are a hardy lot. By necessity, they seem to have better knowledge of a notebook's limitations—and then try to exceed those limits!

This chapter describes several of a notebook's basic components, highlights how each interacts with Linux, and provides tips and pointers on pertinent Linux commands, utilities, and software you can use with the hardware. You need to know a lot about your notebook in order to get the most out of Linux. This information will come in handy later if you're faced with configuration questions. This information also introduces the chapters in Part II, “Managing Your Notebook: Making It Work the Way You Want.”

## Type of CPU

The range of notebooks with CPUs that can be used with Linux now spans early Intel-based 386-compatibles to the latest 700MHz Pentium IIIs. The CPU is undoubtedly the most critical notebook element, but also the most problematic. Fortunately, chip manufacturers such as Intel and AMD are designing CPUs to draw less power and create less heat, a potentially destructive force inside your laptop.

Although desktop computers can be cooled down with auxiliary devices such as extra fans, notebooks are supposed to provide adequate cooling by design. This has not always been the case, however, and models have been produced in which too much heat is generated or in which the CPU heats up so much that the system automatically shuts down as a fail-safe. This problem was endemic with notebooks using desktop versions of CPUs, not CPUs designed for mobile computers. Some desktop CPUs, such as early AMD K-6s and Cyrix 686s, purportedly run much hotter than Intel equivalents. Fortunately, built-in power-saving features preclude any catastrophe and also save energy.

In general, the current crop of laptops use one of five types of CPUs specifically designed for mobile use:

- **Intel Mobile Pentium III** (nicknamed *Coppermine*). Now being manufactured with speeds up to 750MHz, these CPUs use new *packaging*, or
