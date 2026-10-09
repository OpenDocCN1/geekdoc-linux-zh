
## Lesson 8 Lab 1

### Exploring the Kernel Services and Configuration

![](img/477ccb2f05b6ba1b2d563ea74f18c197_935_0.png)

You can find a suggested solution for this activity in the Lesson 8 Lab 1 solution.html file in the Managing_Kernel_Services\Solution folder in the student data files.

**Before You Begin:**
Copy the grub.conf file as grub.conf.bak to make a backup of the grub.conf file.

**Scenario:**
The system administrator is responsible for monitoring the performance of kernels to ensure smooth running of the systems. Therefore, you decide to acquaint yourself with various kernel services and how to configure them.

- 1. Create a new initrd image.
- 2. Update the GRUB configuration with the new initrd image.
- 3. View the new initrd image and boot the system using it.
- 4. View all peripheral devices that are connected to the system.
- 5. View all hardware devices that are connected to the system using the HAL device manager.
- 6. Monitor the processes currently running on the system.

## Lesson 9 Lab 1

### Managing Files Using Basic Bash Shell Operations

You can find a suggested solution for this activity in the Lesson 9 Lab 1 solution.html file in the Working_with_Bash_and_Shell_scripts\Solution folder in the student data files.

**Data Files:**
Software_List.txt, Software_Rules.txt, Software_Audit_Report_08.txt, Software_Audit_Report_09.txt

**Before You Begin:**
Ensure that the required data files are copied into the /root directory.

**Scenario:**
You want to search for documents that you created several months ago. You remember that the names of the files begin with the word “Software.” You want to find them and create a backup of the files in the /mybackup directory.

- 1. Search for file names beginning with “Software.”
- 2. Create a backup of the files in the /mybackup directory.

## Lesson 9 Lab 2

### Use Variables to Configure the Shell Environment

![](img/477ccb2f05b6ba1b2d563ea74f18c197_937_0.png)

You can find a suggested solution for this activity in the Lesson 9 Lab 2 solution.html file in the Working_with_Bash_and_Shell_scripts\Solution folder in the student data files.

**Scenario:**
Your colleague asked you to set up his Linux system with the following requirements.

- Write a script to remind him to fill the effort tracking sheet everyday.
- Assign the *root* directory to the local path in the system.
- The command prompt should reflect the company name, “Our Global Company.”
- Customize the history file size to display only 500 entries on running the *history* command.

- 1. Write a script named Reminder to remind the user to fill his effort tracking sheet whenever he logs in.
- 2. Save and convert the file into an executable script.
- 3. Test the script.
- 4. Customize the environment variables in the *~/bashrc* script file to suit your colleague’s needs.
- 5. Check the changes.

## Lesson 9 Lab 3

### Applying Basic Scripting Techniques

![](img/477ccb2f05b6ba1b2d563ea74f18c197_938_0.png)

You can find a suggested solution for this activity in the **Lesson 9 Lab 3 solution.html** file in the Working_with_Bash_and_Shell_scripts\Solution folder in the student data files.

**Scenario:**
You want to track your daily tasks so that you can fill your weekly timecard easily. You decide to maintain a list, daily work-done, in a text file with unique names. You decide to name each file with the current date, and also add the date as the first line of each file. You want to write a script named dailyupdate to automate this process.

- 1. Create a script file named dailyupdate using Vim.
- 2. Write the code to create text files redirecting the date input from the user.
- 3. Write the code to confirm file creation with a unique file name.
- 4. Test the script.

## Lesson 10 Lab 1

### Performing Process Management

![](img/477ccb2f05b6ba1b2d563ea74f18c197_939_0.png)

You can find a suggested solution for this activity in the Lesson 10 Lab 1 solution.html file in the Managing_Jobs_and_Processes\Solution folder in the student data files.

**Scenario:**

As a system administrator, you have to monitor the processes running on your system and their usage of system resources. You will perform the following tasks everyday.

- List all background jobs.
- Suspend or terminate unnecessary processes.

- 1. Execute three commands as background processes.
- 2. Terminate the last job.
- 3. Bring the second job to the foreground and suspend it.
- 4. Enter *jobs* to view the list of processes running in the background.
- 5. View your current running processes and all other running processes.

## Lesson 10 Lab 2

### Multitasking in Linux

![](img/477ccb2f05b6ba1b2d563ea74f18c197_940_0.png)

You can find a suggested solution for this activity in the Lesson 10 Lab 2 solution.html file in the Managing\_Jobs\_and\_Processes\Solution folder in the student data files.

**Scenario:**

You received several complaints about processes taking longer than usual to complete. There are certain commands that are running with high priority, which can be lowered. Practice altering the command priority and delaying jobs to run at different times. This should free up some processing power so that critical processes can be run.

- 1. View the processes on your system.
- 2. Issue the command to copy installation files as a background process.
- 3. Renice the copy process by using the top command.
- 4. Issue a command to run in the background and log out of the system.
- 5. Log in as root and verify that the job is complete.

## Lesson 11 Lab 1

### Configuring System Services

![](img/477ccb2f05b6ba1b2d563ea74f18c197_941_0.png)

You can find a suggested solution for this activity in the Lesson 11 Lab 2 solution.html file in the Configuring_System_Services\Solution folder in the student data files.

**Scenario:**
You are a system administrator in OGC systems. Your organization has many branches and has already enabled system and network services on the server to allow employees from different branches to communicate and share information. You need to monitor the activities that take place on the server.

- 1. Enable SELinux on srvA.
- 2. Configure syslogd to set up the system to act as a central network log server.
- 3. Configure alerts and warning on logs.

## Lesson 12 Lab 1

### Implementing DNS Service

**Before You Begin:**

- 1. On the system labeled srvB, using the vi editor, open the /etc/sysconfig/selinux file.
- 2. Change SELINUX=permissive to SELINUX=disabled.
- 3. Switch to the command mode. Save and close the file.
- 4. Reboot the system. Switch to the CLI. Log in as root.
- 5. Enter iptables -F to flush the IP tables. Enter iptables -F -t nat to flush the NAT IP table. Enter service iptables save to save the IP tables’ settings.
- 6. Reboot the system. Switch to the CLI. Log in as root.
- 7. Enter yum localinstall /rhelsource/Server/bind* to install the BIND packages. Enter y to continue with the installation. Clear the screen.

**Scenario:**

Your organization opened a new branch. The marketing department uses a server srvB and 50 systems to manage its functions. To facilitate communication and efficient administration, you want to bring all systems under a common domain, ourglobalcompany.com.

The parameters for the forward and reverse zones are given in the table:

| | Forward Zone | Reverse Zone |
| :--- | :--- | :--- |
| TTL value | 86400 seconds | 86400 seconds |
| Serial number | 1001 | 1001 |
| Length of the refresh cycle | 28800 seconds | 28800 seconds |
| Length of the retry cycle | 7200 seconds | 7200 seconds |
| Duration for the slave server to respond to queries | 3600000 seconds | 604800 seconds |
| The default TTL value for negative caching servers | 86400 seconds | 86400 seconds |

![](img/477ccb2f05b6ba1b2d563ea74f18c197_942_0.png)

You can find a suggested solution for this activity in the Lesson 12 Lab 1 solution.html file in the Configuring_Network/Solution folder in the student data files.

- 1. Configure the DNS server for the ourglobalcompany.com domain on srvB.
