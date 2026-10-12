![](bbox=[0.26, 0.08, 0.7, 0.36])

**FIGURE 9.11** KDEprintFax allows you to send faxes from your Linux desktop. It is a GUI front end to Efax, a command-line application.

> **NOTE**
> Using multiple fax applications might seems unnecessarily complicated to fax users who are used to sending and receiving their faxes on their own machine through a modem connected to that machine. The Linux (and Unix) approach is more complicated because it is network focused. A single computer can be set up to send and receive faxes for the entire network of hundreds of computers. None of the individual computers has a need for Efax or a fax modem; they just need a fax reader/viewer and a convenient way to send them a fax document to the central fax server.

The `/usr/bin/fax` script provides a simple command-line interface to Efax that allows you to send, receive, view, or print faxes without a GUI. You can view the commands available for faxing by entering **fax help** at the command line. You can use the **fax make** command to turn a text file into a fax file. Fedora Core also provides the efax command-line application to convert files formats from fax, text, bitmap, and grayscale formats, if necessary. All these applications can be called from scripts to automate the process of converting fax messages, so the end user never has to bother with it.

> **TIP**
> You can find more information on the workings of fax and Efax in the man pages and at the Efax home page at http://www.cce.com/efax/documentation/.

Efax is really designed for a single user; there are other fax applications mentioned here that can handle entire offices. If you have more that one fax user, Efax is likely to be too simple for your needs.