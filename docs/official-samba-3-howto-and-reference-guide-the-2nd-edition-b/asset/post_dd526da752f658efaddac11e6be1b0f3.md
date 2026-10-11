
To switch to other than **Basic** editing ability, click on **Advanced**. You may also do this by clicking on the radio button, then click on the **Commit Changes** button.

After making any changes to configuration parameters, make sure that you click on the **Commit Changes** button before moving to another area; otherwise, your changes will be lost.

![](img/86d74c6cc862465e3a42e6dc3c90935a_633_0.png)

**NOTE**

SWAT has context-sensitive help. To find out what each parameter is for, simply click on the **Help** link to the left of the configuration parameter.

## 36.3.3 Share Settings

To affect a currently configured share, simply click on the pull-down button between the **Choose Share** and the **Delete Share** buttons and select the share you wish to operate on. To edit the settings, click on the **Choose Share** button. To delete the share, simply press the **Delete Share** button.

To create a new share, next to the button labeled **Create Share**, enter into the text field the name of the share to be created, then click on the **Create Share** button.

## 36.3.4 Printers Settings

To affect a currently configured printer, simply click on the pull-down button between the **Choose Printer** and the **Delete Printer** buttons and select the printer you wish to operate on. To edit the settings, click on the **Choose Printer** button. To delete the share, simply press the **Delete Printer** button.

To create a new printer, next to the button labeled **Create Printer**, enter into the text field the name of the share to be created, then click on the **Create Printer** button.

## 36.3.5 The SWAT Wizard

The purpose of the SWAT Wizard is to help the Microsoft-knowledeable network administrator to configure Samba with a minimum of effort.

The Wizard page provides a tool for rewriting the **smb.conf** file in fully optimized format. This will also happen if you press the **Commit** button. The two differ because the **Rewrite** button ignores any changes that may have been made, while the **Commit** button causes all changes to be affected.

The **Edit** button permits the editing (setting) of the minimal set of options that may be necessary to create a working Samba server.

Finally, there are a limited set of options that determine what type of server Samba will be configured for, whether it will be a WINS server, participate as a WINS client, or operate with no WINS support. By clicking one button, you can elect to expose (or not) user home directories.

## 36.3.6 The Status Page

The status page serves a limited purpose. First, it allows control of the Samba daemons. The key daemons that create the Samba server environment are smbd, nmbd, and winbindd. The daemons may be controlled individually or as a total group. Additionally, you may set an automatic screen refresh timing. As MS Windows clients interact with Samba, new smbd processes are continually spawned. The auto-refresh facility allows you to track the changing conditions with minimal effort.

Finally, the status page may be used to terminate specific smbd client connections in order to free files that may be locked.

## 36.3.7 The View Page

The view page allows you to view the optimized **smb.conf** file and, if you are particularly masochistic, permits you also to see all possible global configuration parameters and their settings.

## 36.3.8 The Password Change Page

The password change page is a popular tool that allows the creation, deletion, deactivation, and reactivation of MS Windows networking users on the local machine. You can also use this tool to change a local password for a user account.

When logged in as a non-root account, the user must provide the old password as well as the new password (twice). When logged in as *root*, only the new password is required.

One popular use for this tool is to change user passwords across a range of remote MS Windows servers.

# Part V

# Troubleshooting

# THE SAMBA CHECKLIST

## 37.1 Introduction

This file contains a list of tests you can perform to validate your Samba server. It also tells you what the likely cause of the problem is if it fails any one of these steps. If it passes all these tests, then it is probably working fine.

You should do all the tests in the order shown. We have tried to carefully choose them so later tests only use capabilities verified in the earlier tests. However, do not stop at the first error; there have been some instances when continuing with the tests has helped to solve a problem.

If you send one of the Samba mailing lists an email saying, “It does not work,” and you have not followed this test procedure, you should not be surprised if your email is ignored.

## 37.2 Assumptions

In all of the tests, it is assumed you have a Samba server called BIGSERVER and a PC called ACLIENT, both in workgroup TESTGROUP.

The procedure is similar for other types of clients.

It is also assumed you know the name of an available share in your **smb.conf**. For our examples this share is called *tmp*. You can add a *tmp* share like this by adding the lines shown in Example 37.2.1.

**Example 37.2.1** smb.conf with [tmp] Share

```
[tmp]
        comment = temporary files
        path    = /tmp
        read only = yes
```

![](img/86d74c6cc862465e3a42e6dc3c90935a_639_0.png)

> These tests assume version 3.0.0 or later of the Samba suite. Some commands shown did not exist in earlier versions.

Please pay attention to the error messages you receive. If any error message reports that your server is being unfriendly, you should first check that your IP name resolution is correctly set up. Make sure your `/etc/resolv.conf` file points to name servers that really do exist.

Also, if you do not have DNS server access for name resolution, please check that the settings for your smb.conf file results in dns proxy = no. The best way to check this is with testparm smb.conf.

It is helpful to monitor the log files during testing by using the `tail -F log_file_name` in a separate terminal console (use ctrl-alt-F1 through F6 or multiple terminals in X). Relevant log files can be found (for default installations) in `/usr/local/samba/var`. Also, connection logs from machines can be found here or possibly in `/var/log/samba`, depending on how or if you specified logging in your smb.conf file.

If you make changes to your smb.conf file while going through these test, remember to restart smbd and nmbd.

## 37.3 The Tests

# DIAGNOSING YOUR SAMBA SERVER

1. In the directory in which you store your smb.conf file, run the command `testparm smb.conf`. If it reports any errors, then your smb.conf configuration file is faulty.

![](img/86d74c6cc862465e3a42e6dc3c90935a_639_1.png)

> Your smb.conf file may be located in /etc/samba or in `/usr/local/samba/lib`.

2. Run the command `ping BIGSERVER` from the PC and `ping ACLIENT` from the UNIX box. If you do not get a valid response, then your TCP/IP software is not correctly installed. You will need to start a “DOS prompt” window on the PC to run ping. If you get a message saying “host not found” or a similar message, then your DNS software or /etc/hosts file is not correctly set up. If using DNS, check that the `/etc/resolv.conf` has correct, current, entries in it. It is possible to run Samba without DNS entries for the server and client, but it is assumed you do have correct entries for the remainder of these tests. Another reason why ping might fail is if your host is running firewall software. You will need to relax the rules to let in the workstation in question, perhaps by allowing access from another subnet (on Linux this is done via the appropriate firewall maintenance commands **ipchains** or **iptables**).

> NOTE
>
> Modern Linux distributions install ipchains/iptables by default.
>
> This is a common problem that is often overlooked.

If you wish to check what firewall rules may be present in a system under test, simply run **iptables** *-L -v*, or if *ipchains*-based firewall rules are in use, **ipchains** *-L -v*. Here is a sample listing from a system that has an external Ethernet interface (eth1) on which Samba is not active and an internal (private network) interface (eth0) on which Samba is active:

```
frod:~ # iptables -L -v

Chain INPUT (policy DROP 98496 packets, 12M bytes)
pkts bytes target prot opt in out source destination
187K 109M ACCEPT all -- lo any anywhere anywhere
892K 125M ACCEPT all -- eth0 any anywhere anywhere
1399K 1380M ACCEPT all -- eth1 any anywhere anywhere \n
state RELATED,ESTABLISHED

Chain FORWARD (policy DROP 0 packets, 0 bytes)
pkts bytes target prot opt in out source destination
978K 1177M ACCEPT all -- eth1 eth0 anywhere anywhere \n
state RELATED,ESTABLISHED
658K 40M ACCEPT all -- eth0 eth1 anywhere anywhere
0 0 LOG all -- any anywhere anywhere \n
LOG level warning

Chain OUTPUT (policy ACCEPT 2876K packets, 1508M bytes)
pkts bytes target prot opt in out source destination

Chain reject_func (0 references)
pkts bytes target prot opt in out source destination
```

3. Run the command **smbclient -L BIGSERVER** on the UNIX box. You should get back a list of available shares. If you get an error message containing the string “bad password”, then you probably have either an incorrect *hosts allow*, *hosts deny*, or *valid users* line in your *smb.conf*, or your guest account is not valid. Check
