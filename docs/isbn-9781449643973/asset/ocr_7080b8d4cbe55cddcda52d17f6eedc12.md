The following summarizes the setup, configuration, and equipment needed to perform Lab #7:

+   1. A Virtualized Server Farm with the following components:
+       a. Microsoft DHCP server for allocating student IP host addresses
+       b. A Student and/or Instructor VM workstation
+       c. Fedora Linux Target VM
+   2. Standard onsite student workstation must have the following software applications loaded to perform this Lab:
+       a. VMware Player 3.x
+       b. Microsoft Office 2007 or higher for Lab Assessment Questions & Answers

# ## Recommended Procedures

**Equipment-Based Lab #7 – Student Steps:**
Students should perform the following steps:

+   1. Connect the student-removable hard drive to your workstation
+   2. Boot up the Student VM and Microsoft DHCP VM server to allocate an IP host address
+   3. Enable your DOS command prompt and type “ipconfig” and “ping” your allocated IP host address 172.30.0.\_\_\_ , the DHCP server 172.30.0.10, and the IP default gateway router 172.30.0.1
+   4. Login to the Student VM using the following credentials:
+       Login ID: “Student” (case sensitive)
+       Password: “ISS316Security” (case sensitive)
+   5. From the GNOME Desktop, at the top left side, click on “Applications”-> Systems Tools -> Terminal

**NOTE:** Before the `sudo` & `su` commands can execute as expected, the user account **MUST** be a member of the wheel group with the wheel group granted limited sudo access as directed in **Lab 3**.

# ### Review & Tune the Fedora Linux Server’s Kernel Parameters

+   6. View configured settings for the running kernel. Type the command: `cat /etc/sysctl.conf | less` and press `<enter>`.
+   7. Press the “q” key to exit and return to the command prompt.