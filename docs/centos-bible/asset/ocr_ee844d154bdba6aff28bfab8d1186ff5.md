# Chapter 16

# Setting Up Printers and Printing

S haring printers is a good way to save money and make your printing more efficient. Very few people need to print all the time, but when they do want to print something, they usually need it quickly. Setting up a print server can save money by eliminating the need for a printer at every workstation. Some of those savings can be used to buy printers that can output more pages per minute or have higher-quality output.

You can attach printers to your CentOS system to make them available to users of that system or to other computers on the network. You can configure your CentOS printer as a remote CUPS printer or Samba printer. With Samba, you are emulating a Windows print server.

This chapter describes configuring and using printers in CentOS. It focuses on Common UNIX Printing Service (CUPS), which is the recommended print service for the current versions of CentOS. To configure CUPS printers, this chapter focuses on the Printer Configuration window (system-config-printer command).

When a local printer is configured, print commands (such as lpr) are available for carrying out the actual printing. Commands also exist for querying print queues (lpc), manipulating print queues (lpc), and removing print jobs (lprm). A local printer can also be shared as a print server to users on other computers on your network.

# IN THIS CHAPTER

+   - Understanding printing in Linux
+   - Setting up printers
+   - Using printing commands
+   - Managing document printing
+   - Sharing printers