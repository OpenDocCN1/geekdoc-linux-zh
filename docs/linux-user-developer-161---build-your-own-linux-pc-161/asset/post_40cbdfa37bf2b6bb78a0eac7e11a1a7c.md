
# Orders and shopfront

Let us move to the shopfront and see how the orders are managed. The process is simple: users visit the shop page and select a product. They can then add the items to their cart. Once all added, they click Checkout. On the checkout page, users need to fill in the shipping address and select the payment method. Finally once the payment is succeeded or if the user selects on delivery, the order is completed.

As you can see, all the orders from WooCommerce Orders are shown here. If you have set up the email notification then you also get emails about new orders from you. You can also add orders by the backend. Click on Add Order and the next page appears, [you] fill in the order details.

# Reports

Reports are important to help you understand the business performance of your ecommerce venture. Let's take a look at all the kinds of reports that WooCommerce offers out of the box. By going to WooCommerce Reports on the next page that appears, you can see three types of different reports.

In the Orders tab you can see all the reports about sales, sales by product, sales by category. In the Customers tab you can see reports about checkouts processed by registered users. You can also see the list of customers. The Stock tab allows you to see information about quantities of all the products - you can see which items are stocked the most and the least, and you can also see out-of-stock items.

# 08 Coupons

Another aspect of online shopping is coupons management. Ecommerce websites are known for discounts for your own shop too. To do this, you need to implement this by enabling coupons in the WooCommerce settings where all the coupons will appear at the top of the page. On the next page, you add the coupon details. Coupon code and the description fields are self-explanatory. The rest is simple.

The Discount Type drop-down lets you to set if the code is valid for everything or only to a product in the cart. You can choose a fixed amount or percentage in the previous drop-down. For a coupon valid for time, you can set the coupon expiry date. The Usage section enables you to add restrictions, like individual use only, or Usage Limits allows you to restrict the number of times the coupon can be used or by a certain user.

> Above Once set up, WooCommerce provides users with a standard shopping cart interface

![](img/a54b3b473771472dd2321ddda1014be1_38_0.png)

# Tutorial Snort

## Detect network intruders with Snort

### Take a deep look at this network intrusion detection system and learn to monitor your device's web traffic

![](img/a54b3b473771472dd2321ddda1014be1_39_0.png)

In its sniffer mode, during operation Snort will read packets and display them on the console. In packet logger mode it will be able to log the packets to the disk. In network traffic mode Snort will monitor network traffic and analyze it against the rules defined by the user. In active mode Snort can perform actions based on detected abnormal activity. It is worth noting that Snort has an in-built tool alerting capability.

As expected, Snort can therefore be used to detect various types of attacks such as port scans, buffer overflows, and more. Snort can be performed on many operating systems, including all the major operating systems. Snort doesn't require you to compile any other software to your existing distribution, but it does require that you have root privileges.

To use Snort, you need to configure the network intrusion detection system. All of this is done by the system administrators to any network activity so that they may make appropriate decisions.

Snort is configured in three different modes:

- Sniffer mode
- Packet logger mode
- Network intrusion detection mode

To get started, let's install the Snort package. The first step, as you may know, is to execute the following command in Linux terminal:

```bash
$ apt-get install snort
```

Once the installation is complete, you can check for a successful installation by using the following command:

![](img/a54b3b473771472dd2321ddda1014be1_39_1.png)

Snort is an open source network intrusion detection system, that performs real-time traffic analysis and packet logging to detect and prevent intrusion attacks. It can function as a packet sniffer, a packet logger, and a network intrusion detection system. Snort uses a flexible rules language to analyze traffic against a set of rules, and then alerts the user or logs the traffic in real time to see if any malicious activity is detected.

Snort can be run in various modes, such as sniffer (to view packets), packet logger (to save packets), and network intrusion detection mode (to analyze traffic against rules).

- An alert mode

## -version

Also, note that Snort comes with a very detailed manual and readers are advised to go through this manual to fully understand the system. Another thing to note here is that some packages are much essential if you need to run Snort.

Alerted in the alert file logging your directory (/var/log/ by default, or the directory you specify with the -l). Snort exits with an error if the configuration file or its logging directory does not exist. You can specify which IP address you want to alert, fast, none or UNIX sockets by supplying the -l switch option. If you do not use the -c switch, Snort will not enter alert mode. Additionally, if you use the -c switch, Snort will use the full alert mode by default. The Snort config file is used to store all the configuration rules. The Snort config file contains commented-out instructions on how to use it. Have a quick look at the configurable items of this snort instance.

# Why use Snort?

- apache for the web server
- mysql-server for the database
- phpps for the server-based script
- php-mysql (PHP Extension and Application Repository)

Snort is considered as the first choice for network intrusion detection systems in many countries. Its effectiveness and the many features make it very popular. Open source Snort is easy to use once you learn how to configure it to the needed environments. You can apt-get all of these programs, either one at a time (example, sudo apt-get install apache) or all at once (sudo apt-get install package). As next step, we need to create the set of directories required for successful running of Snort. Use the following commands:

| Variable | Description |
|---|---|
| HOME_NET | Specifies the IP address you are protecting. When you use Snort, you will need to configure your actual home IP address - do not set this to the default value of any. |
| ORACLE_PORTS | Used to specify the port that Snort is listening on. |
| RULE_PATH | Points to the location of the rules file in your system. Typically, rules are stored in /etc/snort/rules, so make sure you use the full path or where the location is. |

```bash
$ snort /snort.conf
$ snort /rules
$ snort /var/log
```

![](img/a54b3b473771472dd2321ddda1014be1_40_0.png)

# Tutorial Snort

Also note that in order to get Snort ready to run, you need to change the default configuration settings to match your local environment and preferences. Further to this, if you want to change the settings of the default configuration file you will need to make those changes. It is very common to include in Snort configuration files instruct Snort to include the information located in Snort's sensor file. Typically, these files contain configuration-related information and behaviors. As expected, the rules themselves are not entered into the configuration file, order to simplify its management. It is important to understand that there are lines added for each alert and these lines show you the following information:

- IP address of the source
- IP address of the destination
- Packet type and useful header information

In order to execute Snort, you can use the following command:

```bash
$ snort -c /etc/snort.conf -l /var/log/snort/
```

With a config file, each alert will be generated in the /var/log directory. This file contains the alerts while Snort was running. Alerts are classified by the type of alert, and Snort will show you a priority for each alert. You can also run Snort to concentrate on the network using the -n option, as shown in the following command.

You can set alert levels in the rules using the following:

<Rule Actions><Protocol><Source IP Address><Source Point><Direction Option><Destination IP Address><Destination port> (rule options)

Let us take a look at the rule structure with an example:

| Structure | Example |
| --- | --- |
| Rule action | alert |
| Protocol | ICMP |
| Source address | any |
| Source point | any |
| Direction operator | -> |
| Destination IP address | any |
| Destination port | any |
| Rule options | (msg:ICMP Packet; sid:477.2) |

```bash
$ snort -c /etc/snort.conf -l /var/log/snort/
```

If you want to be able to restart Snort by sending the SIGUP signal to the daemon, you will need to use path to the Snort binary when you start. You can use type -snort to get a full understanding of the various options that are available within Snort.

Now let's look at how you can use Snort modes as mentioned earlier. Snort can be configured in three ways: sniffer mode, logger mode and network intrusion detection.

In sniffer mode, Snort will be able to print TCP/IP packet alerts to the screen. You can also do this by using the following command:

```bash
$ snort -v
```

# Pre-defined rules

Snort has enough intelligence to read a rule set if the traffic matches the defined condition. When there is a match condition, alert can be logged to a file specified from the command line or shown on the screen. It is a common practice to use the rule sets available on the Snort network home interface is also available. If Snort makes a rule like the following

```bash
log -tp any -> 192.168.1.0/24
```

This log logs to tp traffic coming from any IP address and any source port on our network where the destination port is 23 (corresponding to tcp). Snort is said to be very powerful. There are three base detection actions that Snort can use when a rule matches a pattern: pass; log; alert. Pass rules generate no output. Alert rules generate an output by the user at runtime at command line, and then they will log the packet using the selected logging method to enable alert.

It is best for you to know that there are many third-party tools which have come up in the market and these tools will help in using Snort for various purposes such as administration, performance and log analysis.

```bash
$ snort -dev -1 /log
```

The above command assumes that you have a directory named log in your directory. If it is not the case, Snort will exit with an error message. As expected, in order you will need to tell Snort where relative to the home network. Another useful method for logging is binary mode, and in this mode Snort will log the packets in binary format to a single binary file in the logging directory. The following command shows how binary mode can be used:

![](img/a54b3b473771472dd2321ddda1014be1_41_0.png)

![](img/a54b3b473771472dd2321ddda1014be1_41_1.png)
