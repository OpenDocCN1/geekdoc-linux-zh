+   Connection from an EC2 Instance running on the same AWS account—if you already have an EC2 Instance up and running, you can use it as your client machine. You’ll need to know the name of one of the Security Groups associated with the EC2 Instance. You’ll also need your twelve-digit AWS Account ID.6

+   Connection from a desktop PC or a server—if your MySQL client application runs on your desktop or on an existing server, you can also use it as your client machine. You’ll need to know the machine’s IP address. If your desktop machine is part of a network that uses network address translation (NAT), use an online service such as http://www.whatismyip.org/ to determine the IP address your network presents to the outside world. Use the `ifconfig` command to determine the IP address of your Linux server, or the `ipconfig` command to determine your Windows server’s IP address.

With the necessary information in hand, return to the AWS Management Console and click on **DB Security Groups**. Click on the DB Security Group named **default** and focus your attention on the bottom half of the page.

If you’re planning to connect to your DB Instance from your EC2 Instance, select **EC2 Security Group** and fill in the form appropriately; then press the **Add** button, as seen in Figure 9.7.

| Connection Type | Details | Status | Actions |
| :--- | :--- | :--- | :--- |
| No Authorizations | | | |
| | **Security Group:** | [ ] | |
| [EC2 Security Group v] | **AWS Account ID:** | [ ] | [Add] |
| | [ ] | | |

![](bbox=[0.15, 0.68, 0.86, 0.7])

Otherwise, select **CIDR/IP** and enter an IP address or IP address range in CIDR notation. If you’re connecting from a single address, simply enter that address followed by `/32` (this will ensure that only your machine will have access). If you’re going to be connecting from a range of addresses, you’ll need to ask for the CIDR address from your network administrator. Once you’ve entered the address, press the **Add** button, as shown in Figure 9.8.

6 Log in to the AWS Management Console at http://aws.amazon.com. Your AWS Account ID is labeled Account Number and can be found on any of the pages linked from the Account section of the console (**Security Credentials, Account Activities, or Usage Reports**).