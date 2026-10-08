
You can specify as many as three name servers, so you may add your ISP's name server as an alternative:

```text
search paunchy.net
nameserver 192.168.1.254
nameserver 198.59.115.2
```

Open a **GNOME Terminal** window and run this command.

```text
host cancun
```

You see this result:

```text
cancun.paunchy.net  has  address 192.168.1.121
```

The **host** command provides numerous options that provide more information about your query. For example, you can see information about where the *host* command gets its information. Add the verbose (-v) option to the preceding example and you see this information.

```text
Trying "cancun.paunchy.net"
; ->HEADER<- opcode: QUERY,  status: NOERROR,  id: 18016
;  flags: qr aa rd ra;  QUERY: 1,  ANSWER: 1,  AUTHORITY: 1,
;       ADDITIONAL: 0

;  QUESTION  SECTION:
;cancun.paunchy.net.     IN     A

;  ANSWER  SECTION:
cancun.paunchy.net.     86400  IN  A  192.168.1.1

;  AUTHORITY  SECTION:
paunchy.net.            86400  IN  NS   ns.paunchy.net.1
Received 69 bytes from 192.168.1.120#53  in 263 ms
```

This list describes what the various sections in the preceding output mean.

- **Question section:** You see in the Question section that the query is cancun.paunchy.net. Note that we ask for only the address of cancun but that the search parameter in the resolv.conf file specifies that the paunchy.net domain be appended to cancun. You also see that an A record is part of the query — you're asking for an IP address.
- **Answer section:** This is the answer to your query. The answer includes the host name and domain — cancun.paunchy.net — and its numeric IP address. The Answer section also includes the time-to-live (TTL) value.
- **Authority section:** This data shows where the information was found in the preceding Answer section. You got the answer from the name server — 192.168.1.254 — that you just built.

All the computers on your network can use your DNS server. Your DNS supplies addresses for all internal machines. The server forwards requests for external addresses as necessary.

## Chapter 17

# Securing Your Future

## In This Chapter

- Thinking security
- Preventing intruders
- Updating Red Hat Linux packages
- Deactivating services with chkconfig
- Using the Secure Shell client
- Configuring a Secure Shell server
- Securing your web server with SSL
- Reading logs
- Understanding the security process

Protecting your individual computers and collective network is an essential task in today’s insecure world. Unfortunately, computer and network security is a big, complex job. This chapter boils down that job to some essential functions. We describe several straightforward methods and utilities that bring your security job down to size. Using these ideas makes both your computers and network safer.

This chapter describes security methods and systems. We have chosen several security tools and systems that should give you the most bang for your buck. This chapter provides a starting point for making your computers and network safer. We encourage you to continue learning and evolving your security system.

## Thinking Security

Computer security is best thought of as an ongoing process. No single method, tool, or system — a silver bullet — can magically protect you from the wild-west Internet. Security, like exercise and diet, is just plain hard work.

Because no silver bullet exists, you have to use layers of security measures, called *defense in depth*. Each layer helps to protect the other layers and vice versa. If and when one layer fails, you fall back on the other. You can also add and remove layers as necessary.

Layered security systems and measures fall under three categories:

- **Prevention:** Tools, utilities, and methods prevent any attacks from succeeding. Tools such as passwords and the firewalls we describe in Chapter 8 are under this heading.
- **Detection:** Because not all attacks can be prevented, detecting them, if possible, is essential. Intrusion detection is still more of an art than a science.
- **Process:** Most computer users would prefer to construct a security system and then sit back and forget about it. However, the hacker world changes as fast as the rest of the world, and the systems that work now won’t necessarily work tomorrow. Therefore, you must keep learning and use that knowledge to improve your security.

### An Ounce of Protection: Preventing Intruders

We start by describing how to minimize your chances of being hacked. The following sections describe systems that increase your security:

- **Updating software:** The Red Hat update utility helps keep your computer’s software up to date, which eliminates vulnerabilities as they are discovered.
- **Removing services:** Hackers can’t take advantage of vulnerable software if you don’t use it. Turning off unnecessary services reduces your exposure.
- **OpenSSH and SSL:** Except when viewing garden-variety, nonsecure Web pages, you should never communicate over the Internet (or wireless LANs) without using encryption. The open source SecureShell (SSH) and Secure Sockets Layer (SSL) provide effective encryption for your communications.

We describe each system in this section.

## Reducing vulnerabilities by updating Red Hat Linux packages

Standard hacker operating procedure is simple: Find and then exploit vulnerabilities. The method, simple but effective, works like this: Joe Hacker walks around the Internet, rattling door knobs and occasionally finding one that's open. When no door is unlocked, the hacker looks for easier locks to pick. Your job is to make sure that your doors and windows are locked and not easily picked. Running firewalls, shutting down unnecessary services, and using good passwords ensures that you don't leave anything unlocked. Making sure that your locks are not easily defeated requires constant supervision. Software is now powerful but complex. Complexity breeds bugs, and with bugs come vulnerabilities. Because the only certainties in life are death, taxes, and buggy software, the bugs have to be fixed whenever possible. Everyone needs to continually update software when errors are found and corrected.

Red Hat created an excellent method for updating its software: The Up-to-Date (up2date) system automatically detects new software and installs it for you. Next to using good passwords and firewalls, it's probably the most effective security system you can run.

If you read about the Setup Agent (firstboot) post-configuration process in Chapter 3, you know that one of the Firstboot steps was registering with the Red Hat Network (RHN). You can register one computer with RHN at no cost. With RHN, you gain the ability to use up2date on one computer (you have to subscribe additional machines for a fee). Red Hat configures up2date to install new RPM packages daily.

You can register now if you haven't already done so. Follow these steps:

1. Click the GNOME menu, choose System Tools->Red Hat Network, and enter your root password if you're prompted.
    The Welcome to Red Hat Update Agent window, as shown in Figure 17-1, opens.
2. Click the OK button and the Question dialog box opens.
    You're told that your keyring doesn't contain the Red Hat public key. A keyring system helps maintain the public keys of places you need to securely communicate with. Because this is the first time you have tried to securely connect to the Red Hat Network, you don't have its public key.

Page 242 | Part IV: Revenge of the Nerds

![](img/8c094d1b36276212c03d10d898508a6e_261_0.png)

**Figure 17-1:** The Red Hat Network Configuration window.

3. Click Yes to accept the Red Hat public key. When the Red Hat Update Agent welcome window opens, click Forward.
    The Step 1 window opens.
4. Click the Forward button.
    Or, you can have your lawyer drop by and read the statement to you and then click the Forward button.
5. Enter the username and password you want to use — plus your e-mail address — in the Step 2 Login window. Click the Forward button.
6. When registering for the first time, you have to create an account. In that case, the Step 2: Create a User Account window opens, as shown in Figure 17-2.
7. (Optional) Enter your personal information in the window.
    Red Hat reads the configuration machine off your computer and shows it on the next screen — Step 3: Register a System Profile Hardware.
8. Click the Forward button and the Step 3: Register a System Profile — Packages window opens. It shows the list of the packages installed on your computer.
    The update system compares these packages with the updated packages that Red Hat provides for download.
9. Click the Forward button.
    The Send Profile Information to Red Hat Network window opens. You’re ready to register your computer with Red Hat. Click the Forward button.
