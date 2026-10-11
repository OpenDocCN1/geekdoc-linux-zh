
a focused passive information gathering campaign that leveraged various Google search operators, connected bits of information "piped" into other online tools, and a bit of creative and logical thinking, we found a forum post made by one of the target's employees in a stamp-collecting forum:

```
Hi!
I'm looking for rare stamps form the 1950's - for sale or trade.
Please contact me at david@company-address.com
Cell: 999-999-9999
```

Listing 193 - A forum post

We used this information to launch a semi-sophisticated client-side attack. We quickly registered a stamps-related domain name and designed a landing page that displayed various rare stamps from the 1950's, which we found using Google Images. The domain name and design of the site definitely increased the perceived reliability of our stamp trading website.

Next, we embedded some nasty client-side attack exploit code in the site's web pages, and called "David" during the workday. During the call, we posed as a stamp collector that had inherited their Grandfather's huge stamp collection.

David was overjoyed to receive our call and visited the malicious website to see the "stamp collection" without hesitation. While browsing the site, the exploit code executed on his local machine and sent us a reverse shell.

This is a good example of how some innocuous passively-gathered information, such as an employee engaging in personal business with his corporate email, can lead to a foothold during a penetration test. Sometimes the smallest details can be the most important.

> While "David" wasn't following best practices, it was the company's policy and lack of a security awareness program that set the stage for this breach. Because of this, we avoid casting blame on an individual in a written report. Our goal as penetration testers is to improve the security of our client's resources, not to target a single employee. Simply removing "David" wouldn't have solved the problem.

Let's take a look at some of the most popular tools and techniques that can help us conduct a successful information gathering campaign. We will use MegaCorp One,¹³⁸ a fictional company created by Offensive Security, as the subject of our campaign.

## 6.1 Taking Notes

An information gathering campaign can generate a lot of data, and it's important that we manage that data well so that we can leverage it in further searches or use it in a later phase. There is no right or wrong way to take notes. However, we may find it easier to retrieve information later on if we keep detailed and well formatted notes.

¹³⁸ (Offensive Security, 2019). https://www.megacorpone.com/

## 6.2 Website Recon

If the client has a website, we can gather basic information by simply browsing the site. Small organizations may only have a single website, while large organizations might have many, including some that are not maintained. Let's check out MegaCorp One's website ([https://www.megacorpone.com/](https://www.megacorpone.com/)) to learn more about our target.

![MegaCorp One](img/ec25e59d75726b7041242a56d3376832_136_0.png)

Figure 19: MegaCorp One

A quick review of their website reveals that they are a nanotech company.

The about page at [https://www.megacorpone.com/about.html](https://www.megacorpone.com/about.html) reveals email addresses and Twitter accounts of some of their employees:

![About Us - MegaCorp One](img/ec25e59d75726b7041242a56d3376832_137_0.png)

Figure 20: About Us - MegaCorp One

We could use these addresses in a social media information gathering campaign. We will discuss this in more detail in a later section.

It’s also worth mentioning that the company’s email address format follows a pattern of "first initial + last name". However, their CEO’s email address simply uses his first name. This indicates that founders or long-time employees have a different email format than newer hires. This information could be useful in a later stage of the assessment.

Corporate social media accounts, found on the same page, are also worth recording for further research:

![Social Media - MegaCorp One](img/ec25e59d75726b7041242a56d3376832_138_0.png)

Figure 21: Social Media - MegaCorp One

Let’s update our notes to keep track of each of these bits of information including the email address format and social media sites references.

## 6.3 Whois Enumeration

Whois¹³⁹ is a TCP service, tool, and a type of database that can provide information about a domain name, such as the *name server*¹⁴⁰ and *registrar*;¹⁴¹ This information is often public since registrars charge a fee for private registration.

We can gather basic information about a domain name by executing a standard forward search by passing the domain name, *megacorpone.com*, into the **whois** client:

```bash
kali@kali:~$ whois megacorpone.com
Domain Name: MEGACORPONE.COM
Registry Domain ID: 1775445745_DOMAIN.COM-VRSN
Registrar WHOIS Server: whois.gandi.net
Registrar URL: http://www.gandi.net
Updated Date: 2019-01-01T09:45:03Z
Creation Date: 2013-01-22T23:01:00Z
Registry Expiry Date: 2023-01-22T23:01:00Z

Registry Registrant ID:
Registrant Name: Alan Grofield
Registrant Organization: MegaCorpOne
Registrant Street: 2 Old Mill St
Registrant City: Rachel
Registrant State/Province: Nevada
Registrant Postal Code: 89001
Registrant Country: US
Registrant Phone: +1.9038836342

Registry Admin ID:
Admin Name: Alan Grofield
Admin Organization: MegaCorpOne
Admin Street: 2 Old Mill St
Admin City: Rachel
Admin State/Province: Nevada
Admin Postal Code: 89001
Admin Country: US
Admin Phone: +1.9038836342

Registry Tech ID:
Tech Name: Alan Grofield
Tech Organization: MegaCorpOne
Tech Street: 2 Old Mill St
Tech City: Rachel
Tech State/Province: Nevada
Tech Postal Code: 89001
Tech Country: US
Tech Phone: +1.9038836342

Name Server: NS1.MEGACORPONE.COM
Name Server: NS2.MEGACORPONE.COM
Name Server: NS3.MEGACORPONE.COM
```

Listing 194 - Using whois on megacorpone.com

Not all of this data is useful, but we did discover some valuable information. First, the output reveals that Alan Grofield registered the domain name. According to the Megacorp One Contact page, Alan is the "IT and Security Director".

We also found the name servers for MegaCorp One. Name servers are a component of DNS, which we won't be examining here, but we should add these servers to our notes.

In addition to this standard forward lookup, which gathers information about a DNS name, the whois client can also perform reverse lookups. Assuming we have an IP address, we can perform a reverse lookup to gather more information about it:

```bash
kali@kali:~$ whois 38.100.193.70
NetRange:   38.0.0.0 - 38.255.255.255
CIDR:       38.0.0.0/8
NetName:    COGENT-A

OrgName: PSINet, Inc.
OrgID: PST
Address: 2450 N Street NW
City: Washington
StateProv: DC
PostalCode: 20037
Country: US
RegDate:
Updated: 2015-06-04
```

Listing 195 - Whois reverse lookup

The results of the reverse lookup gives us information on who is hosting the IP address. This information could be useful later, and as with all the information we gather, we will add this to our notes.

### 6.3.1.1 Exercise

- Use the whois tool in Kali to identify the name servers of MegaCorp One.

## 6.4 Google Hacking

The term "Google Hacking" was popularized by Johnny Long in 2001. Through several talks¹⁴² and an extremely popular book (*Google Hacking for Penetration Testers*¹⁴³), he outlined how search engines like Google could be used to uncover critical information, vulnerabilities, and misconfigured websites.

At the heart of this technique were clever search strings and *operators*¹⁴⁴ that allowed creative refinement of search queries, most of which work with a variety of search engines. The process is iterative, beginning with a broad search, which is narrowed down with operators to sift out irrelevant or uninteresting results.

Let’s try a few of these operators and get a feel for how they work.

The *site* operator limits searches to a single domain. We can use this operator to get a rough idea of an organization’s web presence:

¹³⁹ (Wikipedia, 2019) https://en.wikipedia.org/wiki/WHOIS
¹⁴⁰ (Wikipedia, 2019) https://en.wikipedia.org/wiki/Name_server
¹⁴¹ (Wikipedia, 2019) https://en.wikipedia.org/wiki/Domain_name_registrar
¹⁴² References to Johnny Long's talks.
¹⁴³ Reference to "Google Hacking for Penetration Testers".
¹⁴⁴ Reference to search operators.
