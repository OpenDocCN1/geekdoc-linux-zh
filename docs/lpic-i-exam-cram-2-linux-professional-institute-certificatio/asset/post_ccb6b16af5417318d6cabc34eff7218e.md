
## Exam Prep Questions

1. If your IP is **192.168.33.35** and your network mask is /28, what is the address of your local network?

- A. **192.168.33.16**
- B. **192.168.33.32**
- C. **192.168.33.0**
- D. **192.168.33.64**

Answer B is correct because the network is a Class C; therefore, the network mask of /28 causes the LSB to be 16, and networks are incremented by 16, making the **192.168.33.35** address’s network address **192.168.33.32**. Answer A is incorrect because that is the first valid network but not the one that IP resides on. Answer C is incorrect because **192.168.33.0** is the default network if you were using a /24 network mask. Answer D is incorrect because it’s two networks past the one your IP is on.

2. You need to view a user’s routing information on his workstation. Which command, with any needed options, would you use to accomplish this? Write your answer on the blank below:

> The correct answer is *route*. An alternative is *netstat -r*.

3. Your boss wants you to create a subnet scheme that gives your company eight networks with at least 10 hosts per network. Which subnet mask for a Class C leased network address would meet those objectives?

- A. **255.255.255.192**
- B. **255.255.255.224**
- C. **255.255.255.240**
- D. **255.255.255.248**

Answer C is correct because, with the number of networks needed, a **240** subnet mask is needed and allows for at least 10 hosts per network. Answer A is incorrect because a **192** subnet mask allows for only 4 possible networks. Answer B is incorrect because a **224** subnet mask allows for only 8 possible networks, but, with the loss of the first and last subnets, a 224 subnet mask really means that 6 networks are usable. Answer D is incorrect because a **248** subnet mask allows for enough networks (32) but not enough hosts per network.

4. A user is complaining that she can’t reach a Web mail site she frequents, but she can reach other hosts on your networks and on the Internet. Which command would show you where the problem is occurring? Fill in the blank with just the most appropriate command name:

The correct answer is `traceroute`. There are no correct alternative answers.

5. When a user tries to access a server that has recently had its IP changed, he gets a message stating *host not found*. Which of the following commands shows the relationship between that server’s IP and the MAC address of its interface on the network?

- A. `ping`
- B. `arp`
- C. `host`
- D. `nslookup`

Answer B is correct because it shows the IP-to-MAC mapping for a particular host. Answers A, C, and D are incorrect because they have nothing to do with the IP-to-MAC mapping.

6. You are configuring a system and need to set your `eth0` interface to have a default gateway with the address `192.168.33.1`. Fill in the blank with the exact command and options to accomplish this from the command line:

The correct answer is `route add default gw 192.168.33.1`. There are no correct alternative answers.

7. You want to find the mail servers for a particular domain but not see all the address records. Which of the following commands can accomplish this? (Choose all that apply.)

- A. `nslookup`
- B. `host`
- C. `resolver`
- D. `dig`

Answers A, B, and D are correct because they all can be used to show MX records or the names of the mail servers. Answer C is incorrect because there isn’t a command on a default machine named `resolver`.

8. On a Red Hat machine, you need to edit a file that will set the order for how names are resolved. Fill in the blank with the full path and filename for this file:

The correct answer is `/etc/nsswitch.conf`. There are no correct alternative answers.

9. Which of the following is a valid entry for resolution methods on the `hosts:` line in the `/etc/nsswitch.conf` file? (Choose all that apply.)

- A. `files`
- B. `ylwpage`
- C. `dns`
- D. `nis`

Answers A, C, and D are correct because they all are valid resolution methods on the `hosts:` line in the `/etc/nsswitch.conf` file. Answer B is incorrect because there isn't a method named ylwpage.

10. You need to capture data packets from the network for later analysis. Fill in the blank below with only the command name that will accomplish this on a default machine:

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

The correct answer is `tcpdump`. There are no correct alternative answers.

![](img/49f4f38f3aec011238fa50f89e643db3_482_0.png)

## Network Services

### Terms you'll need to understand:

- Aliases
- Caching
- Lookup
- Share
- Smart host
- Wrappers

### Techniques you'll need to master:

- Configuring and managing network services
- Configuring and managing services on demand
- Configuring and operating Sendmail
- Configuring and operating Apache
- Configuring and operating NFS and Samba
- Setting up and configuring name services
- Setting up and using Secure Shell

# Network Services

This chapter is specifically designed to help you configure and manage the services or daemons installed by default on a standard Linux server.

Some of the services covered in this chapter are complete book topics in themselves. LP1's exam objectives (which I must follow and expand upon) don't cover such in-depth knowledge but focus on the ability to configure and manage most basic functions of these services.

The 102 exam assumes you have passed the 101 exam, which means you have a certain level of proficiency with installation and basic configuration. Building on that base of knowledge are the 102 requirements to do basic configuration and management tasks for the various services a typical departmental server would provide.

## Providing Services on Demand

A Linux server can run about any service. Therein lies one of its greatest strengths, and for a weak-willed sysadmin, one of its greatest weaknesses. If you configure your server to provide too many services that run constantly, performance will suffer.

The three strata of service configuration for a server are

- **Always on**—This level is for services that should be running because clients will expect their presence.
- **On demand**—This level is for periodically used services, those that should be present but not on using RAM and CPU constantly.
- **Off or disabled**—This level represents those services that you're not going to run regardless, such as ISDN services on an Ethernet-connected server and so on.

## Using inetd and xinetd

The older of two services, the `inetd` daemon is intended to provide services upon client demand. The idea behind `inetd` is to provide a method to start and run services on demand, particularly to start the service on receipt of a client connection request. The `inetd` configuration file (`/etc/inetd.conf`) contains a line for each service `inetd` controls.

The `xinetd` service is the newer of the two services and provides more atomic control, using a main configuration file (`/etc/xinetd.conf`) to point to a directory (typically `/etc/xinetd.d`) that contains a single text configuration file for each controlled service, such as `/etc/xinetd.d/telnet`.

> **NOTE** Writing about **inetd**/xinetd without switching back and forth in a confusing manner is difficult; therefore, I cover both in one section, splitting into notes and tips when needed or when one deserves more attention. The two services are very similar, with the main difference being the layout of the configuration files.

Although having standard services capable of being started on demand is advantageous, many services require the starting of multiple child processes or the generation of various security keys that make them less likely candidates for being run on demand.

> **ALERT** Some services are **httpd** (which needs to start several to many child processes), **ssh** (which needs to generate keys and so on), and **ssl** (which can also require the generation of keys when starting).

A number of services are governed by `inetd`/`xinetd`; the more familiar of these include

- **finger**—It’s used to provide user login information and is considered to be a security risk.
- **imap**—It’s a daemon that enables users to store their email on a server rather than download it to a client. This is often moved to a full-time service.
- **ktalk**/`ntalk`—These are used to provide chat/instant messenger-type services; they’re not needed very often.
- **rsh**/`rexec`/`rlogin`—The very insecure r services, these should be disabled and replaced by **ssh** and **scp**.
- **telnet**—It’s another insecure service, but one that is frequently used for providing a shell session to a remote client.
- **wu-ftp**d—The most common of the FTP daemons that are present in many distributions, this is often migrated to a full-time service.

If a service is important enough to be available and running, you probably should not have the service governed by `inetd`/`xinetd`. Migrate the service into the `init.d` service directory and start it in the appropriate runlevels via `ntsysv`, `chkconfig`, or `update-rc.d`.
