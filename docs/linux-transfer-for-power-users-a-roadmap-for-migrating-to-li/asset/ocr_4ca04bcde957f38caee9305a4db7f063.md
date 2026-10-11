Because this is an introduction to installing Fedora Core, I'm going to assume that you're not going to want to mess with the boot loader at this point. The "Options" section, later in this chapter, describes what you'll see if you select some of the Boot Loader options.

**Step 14.** In the Boot Loader Configuration screen, simply click Next to move to the next step, the Network Configuration screen, as shown in Figure 29.

![](bbox=[0.08, 0.2, 0.92, 0.53])

Figure 29. The Network Configuration screen allows you to determine how IP addresses and hostnames will be assigned.

# ## Network Configuration

The default choice for the network configuration is DHCP (Dynamic Host Configuration Protocol). This means that the IP address that the computer uses is dynamically assigned by another computer. This is the default for many desktop computers, so we're going to go with it. You can use the Edit button in the upper right corner to assign a static IP address. Details are provided in the "Options" section later in this chapter.

**Step 15.** Click Next to move to the Firewall Configuration screen, as shown in Figure 30.

# ## Firewall Configuration

A firewall is a vehicle for controlling what types of traffic are allowed to access your machine from the network. Fedora Core includes a software firewall that is turned on by default, via the "Enable firewall" option button. You can optionally permit selected services to pass through the firewall by selecting the appropriate check boxes in the middle of this screen.

**Step 16.** Leave "Enable firewall" selected, don't check any of the services or device check boxes in the other sections, and click Next to move to the Additional Language Support screen, shown in Figure 31.