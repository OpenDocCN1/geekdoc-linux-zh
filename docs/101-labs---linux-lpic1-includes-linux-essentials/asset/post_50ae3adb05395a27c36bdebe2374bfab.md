
# LAB 99

## Setup Host Security: Network Services

**Lab Objective:**
Learn how to restrict network services on a Linux host.

**Lab Purpose:**
In this lab you will learn how to securely configure and turn off unused network services.

**Lab Tool:**
Ubuntu 18.04 (or another distro of your choice)

**Lab Topology:**
A single Linux machine, or virtual machine

**Lab Walkthrough:**

### Task 1:

Install xinetd: `sudo apt install xinetd`

`xinetd` is a general network services daemon, or “super-server”; it listens on multiple ports and then filters the connections and launches a listener for the relevant service when needed.

Take a look at some of the default configurations, like `/etc/xinetd.d/echo`. These are internal services and disabled by default; you may find some of the man page examples helpful, in terms of illustrating how you can use `xinetd` to run arbitrary servers (out of shell scripts, etc.)

### Task 2:

Are your `ss` and `nmap` outputs not as clean as they could be? Do you still have an orphaned mail server running from Lab 85? Now you’ll look for and shut down some of these unnecessary services.

Let’s say that in your output from `ss -aptu`, you have a sendmail-mta process running that shouldn’t be there. (You should run the command and pick an unnecessary service for yourself.)

There are no right answers here because the steps depend greatly upon your system and your services, but here are some general guidelines to follow:

- What is the status of the Systemd service, if it exists (`sudo systemctl status ________`)?
- Have you uninstalled the relevant package(s) via the package manager? If so, run `sudo updatedb && sudo locate ________`—an incomplete removal could leave files behind.
- Once the files are gone, you can kill the process with `kill -9 [pid]`
- If you want to keep the service but not have it start automatically, try: `sudo systemctl disable ________`

## Notes:

A `systemd.socket` unit is analogous to `xinetd`, particularly with `Accept=True` in its configuration. Systemd sockets are meant to listen on network sockets in lieu of more resource-intensive services, until those services are actually needed. `xinetd` is still in common use, so Systemd sockets haven’t quite superseded it.

# LAB 100

## Securing Data with Encryption: SSH

**Lab Objective:**
Learn how to operate OpenSSH to create a secure network tunnel.

**Lab Purpose:**
In this lab, you will learn about OpenSSH, a common tool for creating secure connections and tunnels to/from Linux servers.

**Lab Tool:**
Ubuntu 18.04 (or another distro of your choice)

**Lab Topology:**
A single Linux machine, or virtual machine

**Lab Walkthrough:**

### Task 1:

First, install openssh-server: `sudo apt install openssh-server`

Now run: `ssh-keygen -t ed25519`

You can save your user's SSH key in the default location, but make sure to choose a password—you will use this later.

Copy the public key into `authorized_keys` to allow yourself SSH access: `cp .ssh/id_ed25519.pub .ssh/authorized_keys`

Finally, get your machine's host keys:
`ssh-keyscan localhost | ssh-keygen -lf -`

Save the bottom three lines somewhere; those are your host key fingerprints, in different formats, and you will use one of them later.

### Task 2:

Now run:

- `eval $(ssh-agent)`
- `ssh-add`
- Type your password. This will cache your **SSH private key** to `ssh-agent` so you don't have to type the password again during this session (while maintaining its security).

Finally, connect with **SSH**: `ssh localhost`.

You should be prompted to confirm a previously unknown host key. Compare this key with the three host keys you saved from Task 1; one of them should be a match. (If not, something has gone wrong.) Assuming so, confirm the connection and you should now be connected locally over SSH, without having to type your password again.

### Task 3:

Run `exit`, then run `ssh localhost` again just to be sure you can connect with no prompts.

Now run:

- `exit`
- `kill $SSH_AGENT_PID`
- `ssh localhost`

Did you have to type your password this time to unlock your key?

## Notes:

Make sure you can follow and understand all the steps that are happening in this fairly complex process:

- Installing the OpenSSH server. This step generates host keys automatically.
- Generating a keypair for your user, and granting yourself access by creating an `authorized_keys` file containing the public key.
- Getting the server's host key fingerprints for later verification.
- Initializing the `ssh-agent` caching tool and adding your private key to it.
- Connecting over **SSH** (even if to localhost), verifying the host key, and permanently saving the fingerprint.

# LAB 101

## Securing Data with Encryption: GPG

**Lab Objective:**
Learn how to operate GPG for data encryption and verification.

**Lab Purpose:**
In this lab, you will learn about GnuPG, a tool used to encrypt, decrypt, sign, and verify data of files, e-mails, and package updates, among other things.

**Lab Tool:**
Ubuntu 18.04 (or another distro of your choice)

**Lab Topology:**
A single Linux machine, or virtual machine

**Lab Walkthrough:**

### Task 1:

Open the Terminal and run: `gpg --generate-key`
You will be prompted for a name and e-mail address, then GPG will do the rest. Afterwards, run `gpg --generate-key` again to create a second key for a different fictitious person.
List the keys you created with `gpg -k`
Finally, take a peek at `~/.gnupg`. In this directory, you should see a trust database (`trustdb.gpg`) and public keyring (`pubring.kbx`), as well as an `openpgp-revocs.d` directory for revocation certificates, and `private-keys-v1.d` directory containing your private key files.

### Task 2:

Now let’s try sending a secret message between your two imaginary GPG users:

- `echo "Hello World" > secret`
- `gpg -se -r [email1|2] secret`
- `file secret.gpg`
- `gpg -d < secret.gpg`

In this scenario, a file has been sent from [email1] to [email2]. You signed and then encrypted the file with the second user’s public key; secret.gpg was the result, which, as file should tell you, is a PGP RSA encrypted session key. Finally, you decrypt this file and are shown an encryption header, and the message itself, followed by a signature (which GPG informs you is good).

## Notes:

In a real-world scenario, you would be importing keys either from a third-party directly or from a public keyserver, and then assigning them trust values. “Trust” in GPG-speak means “How much do you trust this person to properly verify someone else’s key before signing it?” Recommended research: the web of trust.

Made in the USA
Coppell, TX
10 October 2020

![](img/64f3c5d0defa97e8b856b229f9322b97_265_0.png)

39600376R00144

*Experts agree that we only retain 10% of what we read, but 90% of what we do. Perhaps this explains why the global pass rate for most IT exams is a ghastly 40%. This is where the 101 Labs book series can help.*

*101 Labs’ mission is to turn you into an IT expert by doing instead of reading. Our experts take you by the hand, and walk you through every aspect of the protocols and technologies. We share our configuration tips and tricks, as well as how to avoid common mistakes many novice engineers make which can quickly end a career.*

*By the end of this book, you will have configured more protocols and services than most network engineers get to do in five years. You will be prepared for tough Linux LPIC1 and Linux Essentials exam questions, as well as practical scenarios, technical interviews, and of course real-world issues you will encounter on the job.*

*Since 2002, we’ve been helping people just like you pass IT exams and enjoy rewarding careers in the IT industry. Let us help you too.*

## 101 Labs – Linux LPIC1 has been created to help you pass your exam and prepare you for the real world of internetworking.

It is broken down into LPI Essentials and then the two LPI Administrator exams. You will learn how to:

- Configure files and directories
- Use pipes and redirection
- Configure system logging
- Manage file permissions
- Install a boot manager
- Create, monitor and kill processes
- Write simple scripts
- Maintain system time
- Troubleshoot network issues
- Manage printers and printing errors
- Configure IPv4 and IPv6
- Configure DNS
- Secure data with SSH
- And much more

### About the Author

In 2004, Paul Browning left a career behind in law enforcement, and started an IT consulting and training company through his books, classroom courses, and websites has trained tens of thousands of people from all walks of life.

**Arturo Narváez Bello**
A Linux enthusiast, network engineer at KLA, T1/2, IxiaNet II, consultant since 2014, NOC, and IETF contributor.
