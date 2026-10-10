The following summarizes the setup, configuration, and equipment needed to perform Lab #8:

+   1. A **Virtualized Server Farm** with the following components:
+      a. Microsoft DHCP server for allocating student IP host addresses
+      b. A Student and/or Instructor VM workstation
+      c. Fedora Linux Target VM

+   2. Standard onsite student workstation must have the following software applications loaded to perform this lab:
+      a. VMware Player 3.x
+      b. Microsoft Office 2007 or higher for Lab Assessment Questions & Answers

# Recommended Procedures

**Equipment-Based Lab #8 – Student Steps:**

Students should perform the following steps:

+   1. Connect the student-removable hard drive to your workstation
+   2. Boot up the Student VM and Microsoft DHCP VM server to allocate an IP host address
+   3. Enable your DOS command prompt and type “ipconfig” and “ping” your allocated IP host address 172.30.0.___ , the DHCP server 172.30.0.10, and the IP default gateway router 172.30.0.1
+   4. Login to the Student VM using the following credentials:
+      Login ID: “student” (case sensitive)
+      Password: “ISS316Security” (case sensitive)
+   5. From the GNOME Desktop , at the top left side, click on “Applications”-> Systems Tools -> Terminal

> **NOTE:** For proper completion of this lab your Fedora 14 VM will require a **LIVE** Internet connection. Do **NOT** disconnect the student workstations from the classroom network and Internet connection.

> **NOTE:** Before the sudo & su commands can execute as expected, the user account **MUST** be a member of the wheel group with the wheel group granted limited sudo access as directed in Lab 3.

# Using RPM to Perform Software Management Tasks

+   6. View all files associated with the sendmail package .Type the command: rpm -ql sendmail | less and press <enter> Use the up & down arrow keys to scroll.