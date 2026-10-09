![](bbox=[0.35, 0.08, 0.78, 0.33])

**Figure 13-1** The Print Settings window

system boots (permanently) and on the running system; see page 906 for information on firewall-cmd.

```
    # firewall-cmd --add-port=631/tcp
    # firewall-cmd --permanent --add-port=631/tcp
    # firewall-cmd --add-port=631/udp
    # firewall-cmd --permanent --add-port=631/udp
    # firewall-cmd --add-port=80/tcp
    # firewall-cmd --permanent --add-port=80/tcp
```

PDF printer  You can set up a virtual PDF printer by installing the cups-pdf package, or you can set up this printer manually.

# The System Configures a Local Printer Automatically

In most cases, when you connect a printer to the local system and turn it on, the system displays a message as it installs drivers. When the drivers are installed, the printer is ready for use. Two graphical tools allow you to add and modify printers as well as work with print jobs. You can use Printers from the Settings window (page 107) for most work with printers and system-config-printer (next) for more complex printer-related tasks. Use one of these tools to verify that the printer is installed, send a test page to the printer, and change the configuration of the printer.

# JUMPSTART I: CONFIGURING A PRINTER USING system-config-printer

The Print Settings window (Figure 13-1) enables you to add, remove, and configure local and remote printers. Open this window by giving the command system-config-printer from an Enter a Command window (ALT-F2) or a terminal emulator. This JumpStart