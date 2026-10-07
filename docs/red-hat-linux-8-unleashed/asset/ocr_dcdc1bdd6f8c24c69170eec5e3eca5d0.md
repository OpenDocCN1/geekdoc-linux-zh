# CHAPTER 12

# Printing Services

# IN THIS CHAPTER

+   - Overview of Red Hat Linux Printing

+   - Configuring and Managing Print Services

+   - Creating and Configuring Local Printers

+   - Creating Network Printers

+   - Console Print Control

+   - Using the Common Unix Printing System (CUPS)

+   - Avoiding Printer-Support Problems

+   - Reference

Red Linux supports more than 600 printers from more than 40 manufacturers, and it is possible to mix and match printing hardware with newer computers. In this chapter, you learn about printing services offered in Red Hat Linux. You'll see that Linux can be put to work right away as a print platform, for use by local or remote Linux, UNIX or Windows workstations.

You learn about the many programs, files, and directories that are internal to supporting printing under Red Hat Linux. The chapter also shows simple techniques for configuring new printers in Red Hat Linux. You learn a variety of methods for making printers available for use quickly and easily in Red Hat Linux, and you learn some important workarounds for connecting printer and system hardware with differing port configurations.

Red Hat provides two different print systems you can use to print files: LPRng and the Common Unix Printing System (CUPS). You can use one or the other, but not both as the basis for printing when using Red Hat. This chapter focuses on using LPRng, but a section is devoted to setting up, configuring, administering, and using CUPS for printing. You can switch back and forth between LPRng and CUPS by using Red Hat's graphical redhat-switch-printer utility (discussed later in this chapter).

# Overview of Red Hat Linux Printing

Red Hat's new and revised print filter system is the main engine that enables the printing of many types of documents using Linux. The heart of engine is the GNU GPL version of Aladdin, Inc.'s gs client. The Red Hat system administrator's printer configuration tool is the redhat-config-printer client.