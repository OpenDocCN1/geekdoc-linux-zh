
## Practice Questions

### Question 1

Which of the following commands is used to set up an install server?

- a. `setup_install_server`
- b. `setup_install_server -b`
- c. `install_server setup`
- d. `server_setup -i`

Answer a is correct. The `setup_install_server` command is used to set up an install server. The `-b` command-line argument is used to install a boot server. Therefore, answer b is incorrect. The commands in answers c and d do not exist.

### Question 2

Which of the following is a reason to set up a boot server on a system separate from an install server?

- a. A boot server cannot reside on an install server.
- b. One or more install clients are not on the same subnet as the install server.
- c. All install clients are not on the same subnet.
- d. NIS or NIS+ cannot locate a boot server that resides on an install server.

Answer b is correct. If one or more install clients are not on the same subnet as the install server, you should set up a boot server on a system separate from the install server. A boot server can reside on an install server. Therefore, answer a is incorrect. The location of clients in relation to other clients does not determine the need for boot servers; the location of clients in relation to the install server determines the need for a separate boot server. Therefore, answer c is incorrect. NIS and NIS+ do not locate anything; they serve only as databases of information. Therefore, answer d is incorrect.

### Question 3

Enter the name of the command (without command-line arguments) used to add install client information to an install or a boot server.

The correct answer is `add_install_client`.

### Question 4

Which of the following install methods can use over-the-network installation resources? (Select all that apply.)

- [ ] a. Custom JumpStart
- [ ] b. Web Start
- [ ] c. JumpStart
- [ ] d. Interactive installation

Answers a, b, c, and d are correct. All four installation methods can use over-the-network installation resources.

### Question 5

Which of the following are automatic installation methods? (Select all that apply.)

- [ ] a. SunInstall
- [ ] b. Custom JumpStart
- [ ] c. Web Start
- [ ] d. JumpStart

Answers b and d are correct. Custom JumpStart and JumpStart are automatic installation methods. SunInstall and Web Start are interactive installation methods. Therefore, answers a and c are incorrect.

### Question 6

Enter the name of the command used to add the contents of the Solaris 8 Software (2 of 2) CD or the Solaris 8 Languages distribution CD to an install server.

The correct answer is `add_to_install`.

### Question 7

Which of the following files should be in a JumpStart configuration directory? (Select all that apply.)

- [ ] a. One or more JumpStart profile files
- [ ] b. `check`
- [ ] c. `rules` file
- [ ] d. `rules.ok` file

Answers a, c, and d are correct. The profile files and the rules file are the two types of files that must be created in the JumpStart configuration directory. If they are set up correctly, the rules.ok file is created in the JumpStart configuration directory. The check command, which is located on the Solaris 8 distribution CD, must be executed to validate the rules and profile files. Therefore, answer b is incorrect.

### Question 8

Match each `add_install_client` command-line argument with its purpose.

| Argument | Purpose |
| --- | --- |
| a. `-c` | 1. Specifies the install server and path |
| b. `-d` | 2. Specifies the profile server and JumpStart configuration directory path |
| c. `-p` | 3. Specifies client is a DHCP client |
| d. `-s` | 4. Specifies the server and path for the sysidcfg file |

Answers a-2, b-3, c-4, and d-1 are correct. The `-c server:path` command-line argument specifies the profile server and JumpStart configuration directory where the rules and profile (class) files reside. The `-d` command-line argument specifies that the client will use DHCP to determine the IP address, netmask, and so on. The `-p server:path` command-line argument specifies a server and the full pathname to the sysidcfg file. The `-s server:path` command-line argument specifies the install server and path to the install images.

### Question 9

Enter the file a custom JumpStart installation uses to define how a system is installed.

The correct answer is profile.

### Question 10

Which of the following are Solaris 8 software groups? (Select all that apply.)

- [ ] a. Entire Distribution
- [ ] b. Basic
- [ ] c. End User Support
- [ ] d. Java Development Environment

Answers a and c are correct. Entire Distribution and End User Support are Solaris 8 software groups. The groups in answers b and d do not exist.

### Question 11

Enter the name of the file that contains boot parameters and is updated by the `add_install_client` command.

The correct answer is `/etc/bootparams`.

## Need to Know More?

![](img/b957f979417d9f16274c2eb52c8f2c9f_464_0.png)

Becker, George, Mary E. S. Morris, and Kathy Slattery, *Solaris Implementation* (Prentice Hall, Englewood Cliffs, NJ, 1995), ISBN 0-13-353350-6.

![](img/b957f979417d9f16274c2eb52c8f2c9f_464_1.png)

Sun Microsystems, *Solaris Advanced Installation Guide*. Available in printed form (part number 806-0957-10), on the Web at **http://docs.sun.com**, and from the online documentation, AnswerBook2, provided with the Solaris 8 operating system.

![](img/b957f979417d9f16274c2eb52c8f2c9f_464_2.png)

Sun Microsystems, *System Reference Manual, Section 1—User Commands*. Available in printed form (part number 806-0624-10), on the Web at **http://docs.sun.com**, and from the online documentation, AnswerBook2, provided with the Solaris 8 operating system.

![](img/b957f979417d9f16274c2eb52c8f2c9f_464_3.png)

Sun Microsystems, *System Reference Manual, Section 1M—Administration Commands*. Available in printed form (part number 806-0625-10), on the Web at **http://docs.sun.com**, and from the online documentation, AnswerBook2, provided with the Solaris 8 operating system.

![](img/b957f979417d9f16274c2eb52c8f2c9f_464_4.png)

Sun Microsystems, *System Reference Manual, Section 4—File Formats*. Available in printed form (part number 806-0633-10), on the Web at **http://docs.sun.com**, and from the online documentation, AnswerBook2, provided with the Solaris 8 operating system.

## Sample Test II

![](img/b957f979417d9f16274c2eb52c8f2c9f_465_0.png)

This chapter provides 61 questions on the topics pertaining to Exam CX-310-012, “Certified Solaris Administrator Examination for the Solaris 8 Operating Environment, Part II.” This exam must be completed in 90 minutes.

Keep in mind that to become certified, you must pass both the CX-310-011 exam and this one. The sample test for the CX-310-011 exam is in Chapter 11. See that chapter for test-taking tips as well.

## Sample Test

### Question 1

Enter the name of the command used to add the contents of the Solaris 8 Software (2 of 2) distribution CD to an install server.

### Question 2

Which of the following virtual devices or RAID levels does DiskSuite support? (Select all that apply.)

- [ ] a. Concatenated virtual device
- [ ] b. RAID level 0
- [ ] c. RAID level 1
- [ ] d. RAID level 5
- [ ] e. RAID level 10

### Question 3

Which of the following commands is used to set up a system to be installed over the network?

- ( ) a. `setup_network_client`
- ( ) b. `network_install`
- ( ) c. `add_install_client`
- ( ) d. `install_network_client`

### Question 4

Which of the following /etc/nsswitch.conf file entries would cause DNS, then NIS+, followed by the /etc files, to be searched when trying to resolve a host-name?

- ( ) a. `hosts: dns nisplus files`
- ( ) b. `hosts: files nisplus dns`
- ( ) c. `ipaddress: files nisplus dns`
- ( ) d. `ipaddress: dns nisplus files`
