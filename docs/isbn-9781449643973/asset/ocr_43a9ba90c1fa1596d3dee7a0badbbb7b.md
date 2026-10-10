# Laboratory #9

# Lab #9: Implement Best Practices for Security Logging & Monitoring

# Learning Objectives and Outcomes

Upon completing this lab, students will be able to complete the following tasks:

+   - Configure remote logging in the Fedora Linux Server and send syslogs and other events to a remote host for secure secondary logging
+   - Search through different log files in Fedora Linux Server to identify where certain types of logs are stored and how often they get recycled
+   - Install and configure Tripwire file integrity tool so that modifications to important system files is quickly identified and properly logged both locally and remotely
+   - Install and schedule rkhuntor to run at said interval using the cron subsystem so that a rootkit can be properly and quickly identified if possible
+   - Configure both automatic searches on log files as well as automatic running of important security applications to properly monitor a Fedora Linux Server for malicious activity

# Required Setup and Tools

This lab does not require the use of the Mock IT Infrastructure - Cisco core backbone network. In addition, the Instructor VM workstation and Student VM workstations should be physically disconnected from the internal network and be isolated on the classroom dedicated layer 2 switch. This will allow for a shared DHCP server to be used to allocate the IP addresses for the instructor and student workstations.

The following is required for this equipment-based lab:

+   A) A classroom workstation (with at least 2 Gig RAM) capable of supporting the removable hard drive with the VM server farm connected to the classroom layer 2 switch.
+   B) An instructor workstation (with at least 4 Gig RAM recommended) that shall act as the Instructor's demo lab workstation. The instructor will display the Instructor workstation on the LCD projector to demo the loading and configuring of the Instructor VM workstation using VMware Player.
+   C) Students Lab workstations will use their own VM server farm and VM student workstation. VMware Player will be used to run the Student VM and the Target VM.