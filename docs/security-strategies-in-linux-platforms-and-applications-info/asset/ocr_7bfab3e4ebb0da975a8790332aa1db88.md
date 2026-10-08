# CHAPTER 9 | Networked Application Security

# Commercial Sendmail

Eric Allman, the creator of the open source sendmail server, founded Sendmail, Inc. sponsors developers who work to extend the product into the enterprise. In addition, Sendmail, Inc. has created a number of commercial products with commercial code. Most of this code is eventually released as open source software and integrated into open source sendmail. Nevertheless, commercial Sendmail is a different product.

As suggested at http://www.sendmail.com/sm/solutions/, commercial Sendmail products are available in four areas:

+   * Gateway protection—Includes options to filter, process, and control messages before they are accepted on the network.
* Inbound protection—Specifies requirements for clean and authenticated e-mail messages.
* Outbound protection—Supports compliance of outgoing e-mail messages to organizational policies.
* Internal protection—Addresses multiple domains on the same network.

As you can see, the functionality of commercial Sendmail products in many ways goes beyond that of the open source sendmail software.

# The Postfix Alternative

Because of the complexity of open source sendmail software, many administrators prefer alternatives. One relatively popular open source alternative is Postfix. It's the default MTA for the Ubuntu and SUSE Linux distributions. Methods for configuring Postfix vary. For example, on Ubuntu systems, the following command provides a number of prompts for configuring this MTA:

```
# dpkg-reconfigure postfix
```

Basic options include the following:

+   * Internet site—Configures Postfix to send and receive e-mail using SMTP.
* Internet with smarthost—Integrates the protocol MTA with Postfix.
* Satellite system—Sets Postfix to transmit e-mail to a different system.
* Local only—Limits the Postfix configuration to users on the local system.

This section assumes you've selected Internet with smarthost, the most capable of the Postfix options. Once selected, you are prompted for the following information:

+   1. The domain name covered by this Postfix server, such as example .org
2. The relay host for outgoing e-mail, as an SMTP server for an ISP (if this e-mail server is not a satellite system, you may choose to leave this blank)
3. An e-mail address of the actual mail system administrator