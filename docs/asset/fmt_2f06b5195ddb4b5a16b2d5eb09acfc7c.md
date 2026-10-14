
After a brief introductory screen, you should click `Forward` to move to the Network Device setup. In the Detected Devices drop-down box, select the network interface that is connected to the internet – this is commonly `eth0`. If you know that your IP address is assigned dynamically by your internet router, then check the `IP address is assigned by DHCP` box. Click `Forward` to continue.

You’re probably using a router to connect to the internet, so you won’t need to enable connection sharing. However, if you are using your computer as the gateway to the internet, you should enable this setting and choose the network device that is connected to the local network. You can also choose to use `DHCP` to assign addresses dynamically to the local network, but you will need to have installed the `dhcp3-server` package prior to starting the Firestarter configuration.

![](img/afd38ba98c33e56aa8435c9f1db6bed0_97_2.png)

The final screen prompts you to save your options and start the firewall. If for some reason you don’t wish to start the firewall at this point, un-tick the `Start Firewall Now` check box and click the `Save` button.

## Password hacking

### How outsiders get your passwords

In Ubuntu, the user details are usually stored in `/etc/passwd` along with the numeric `User ID` and `Group ID`. The actual password is not stored here – instead you’ll see a small `x` when looking at this file, which denotes that there is a password present. The actual passwords are stored in an encrypted format within `/etc/shadow`, which will look like gibberish if you try to view it and will not resemble your true password. However, if an outsider manages to get a hold of this file then they can use a number of freely available tools to try to extract this password information. Usually these tools rely on what are known as dictionary-based tools, in that they have a large collection of dictionary words that they use to try and unlock your password information. The tools will literally cycle through all the words available, as well as common misspellings, in an attempt to match one of them with your password. By using the technique that we showed you to create a strong password, you will minimise the risk of any dictionary-based attack as your password will not be based on a dictionary word.

![](img/afd38ba98c33e56aa8435c9f1db6bed0_98_0.png)

**4** Firestarter has now activated the firewall – you can see in the Active Connections area that there is a current connection from the machine to a remote `NFS` server. Firestarter also keeps track of the amount of data that has been sent and received, as well as the current data transfer rate.

![](img/afd38ba98c33e56aa8435c9f1db6bed0_98_1.png)

**5** To define our firewall policy, click the `Policy` tab in the Firestarter window. You can either allow all traffic for a specified network address or address range, or you can allow specific services. We'd recommend allowing specific services where necessary, as this minimises the chances of attack from a local machine.

![](img/afd38ba98c33e56aa8435c9f1db6bed0_98_2.png)

**6** You can either select from the list of services using the drop-down menu, or you can manually enter the port number. Firestarter does a lookup against the `/etc/services` file to give the port its related service name. You are also able to define exactly who can access that particular port.

![](img/afd38ba98c33e56aa8435c9f1db6bed0_98_3.png)

**7** The last step is to apply the new policy, which you do by clicking the `Apply Policy` button in the toolbar. Firestarter will restart the firewall and you will now be able to connect to your machine on that port.

## 获取更多软件

## 添加新软件——免费！

Ubuntu 默认的软件选择已经足够实用，但实际上还有成千上万个软件等待安装。我们来告诉你怎么做...

如果你已经读到杂志的这一部分，你现在应该已经明白 Linux 为你提供了大量的选择来完成特定任务。举例来说，网页浏览器：在 Linux 上你可以获得 Firefox、Opera、Konqueror、Epiphany、Lynx、Links、Amaya、Mozilla、Kazehakase、Galeon、Dillo、Chimera 等等。需要说明的是，这些都是真实的、可用的网页浏览器，并且正在积极开发中，这意味着你可以全部尝试，找到最适合你的那一个。
