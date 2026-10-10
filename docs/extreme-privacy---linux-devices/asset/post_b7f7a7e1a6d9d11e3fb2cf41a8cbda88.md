
## CHAPTER SEVEN: VoIP SERVICE

Now that you have your computer configured as privately and securely as possible, you may want to use it for traditional telephone calls over your internet connection. As explained in my previous digital guide about mobile devices, I never want to rely on the number associated with my mobile device for my daily communications. Therefore, we will need a way to make and receive standard telephone calls and text messages without using our cellular plans. Within GrapheneOS (mobile), I relied on an application called Signetice and various Voice over Internet Protocol (VoIP) providers for all telephone calls. Desktop Linux systems will rely on an application called Linphone for use with these same providers. Before we configure our devices, let's understand the reasons we should be careful about true cellular number usage.

- When you make calls and send text messages through your standard cellular number, there is a permanent log of this activity stored by the provider of your service. This log identifies all of your communications and can be accessed by employees, governments, and criminals. I have witnessed call and text logs be used as the primary evidence within both criminal and civil trials.

- Your cellular telephone number is often used as a primary identifier for your account. If I know your number, I can use this detail to obtain further information such as location history of the mobile device. Your cellular provider stores your location at all times based on the cell towers to which you connect. I can abuse court orders to obtain these details or hire a criminal to breach your account. In past years, we have learned about the ability of bounty hunters to locate mobile devices in real time by simply knowing the cellular number. No court order was required. Journalists have been able to track people's movements for years.

- Cellular telephone numbers are prone to SIM-swapping attacks. If I know your primary number, I can take over your account through various tactics and become the new owner of the number. I can portray you and receive communications meant for you. If you used that number for two-factor authentication, I now have the second factor.

- When you give your telephone number to your friends and family, they will likely store it in their contacts and associate your name with the entry. Someone will then download a nefarious app which requests access to the contact list, sending the contacts to online databases which can be queried. We have seen this with several apps in the past, including caller ID services such as TrueCaller and Mr. Number, which shared private contact details with the world. Have you ever received an email from LinkedIn asking you to connect with someone you knew? This happens when that person agrees to share their contacts, including email addresses and telephone numbers, with the service. Twitter also wants to obtain these details from any members willing to share them. It only takes one instance to make your cell number publicly attached to your true name.

Using VoIP numbers eliminates much of these concerns. Consider the following.

- VoIP calls and messages are also logged within the VoIP provider's portal.
- However, we have more control of this information, and possess options to permanently purge content whenever desired.
- VoIP communications do not possess the same location details as cellular connections. While the VoIP provider might possess an IP address for the connection, there are no cellular towers which provide exact GPS coordinates. If you break into my VoIP account, you will never learn my true location.
- Illegally overtaking a cellular account is trivial today. It can be done within an hour. Porting a VoIP number into another provider can take over a week, and notification of this action will allow you to stop it. Whenever I am forced to use a telephone number for two-factor authentication, I always prefer a VoIP number over a cellular account.
- You cannot stop your friends and family from sharing your telephone number with abusive applications and services. If they only know your VoIP number, there is less risk. Once a VoIP number is publicly leaked with association to your real name, you can easily change it if desired. If you have multiple VoIP numbers, you can isolate them for various uses. When the world knows a VoIP number belongs to you, it cannot be abused in the same way cellular numbers can. Again, VoIP numbers cannot share your location.

The solution to all of this is to never use a true cellular number. Instead, we will only use VoIP numbers for all calls and standard text messages. In the following pages, I explain how to configure various VoIP services for telephone calls and SMS messages. My goal is for you to create your own VoIP product which allows you to make and receive telephone calls on your new secure Linux device at minimal cost. Furthermore, the numbers will be in your control. You will not need to maintain access to a Google Voice account in order to enjoy the benefits of VoIP calls.

This section is technical, but anyone can replicate the steps. As with all online services, any of these steps can change without notice. It is probable that you will encounter slight variations compared to my tutorial during configuration. Focus on the overall methods instead of exact steps. The following explains every step I took in order to create my own VoIP solution with Twilio. Afterward, I present other options which may be more appropriate for some readers. Please read the entire chapter before making any decisions. Most of this chapter is identical to the VoIP content within the mobile and macOS guides previously released.

Before we dive into various options, we must take a quick detour and discuss domain registration. I encourage you to digest this next portion before moving on. The steps you take now might make everything much easier later.

## Domain Registration

In past writings, I explained ways to use anonymous email forwarding services and temporary access providers when registering for online services. I supplied tutorials for providing these masked and disposable addresses to various services to protect our privacy. Today, I believe you should establish a new domain for use with your new private and secure Linux device. Many privacy-focused email services are actively blocked by online providers. If you try to use a SimpleLogin masked email address to open a new line of cellular service, it will probably be blocked. If you try to fool a VoIP provider into accepting a Mailinator or 10MinuteMail address for a new account, expect an immediate suspension. Because of this, I want to have unlimited acceptable email addresses associated with a recognizable domain as I continue to configure my Linux device.

You could simply buy a new domain such as vandyalay-industries.net and configure it for email access, but that may not be the best idea. Many VoIP service companies are now scrutinizing new accounts. If you register with a brand-new domain, they can see that. Many fraud prevention systems block any registrations from domains which were created in the past 30 to 60 days. Therefore, I prefer existing domains which have recently expired and been dropped from their registrar.

First, I navigate to expireddomains.net and then click the "Deleted Domains" tab. I then sort by the following categories until I see desired domain structures.

- BL: Number of known backlinks
- ABY: The first year the domain was seen at Archive.org
- ACR: Number of Archive.org crawl results
- Reg: Number of Top Level Domains (TLDs) which match the domain

Below is an example of a few random results. While two of these have some internet history, none of them look like a traditional business domain which would pass human scrutiny. I only acquire ".com" addresses for this purpose, as some providers block newer TLDs such as ".work".

| Domain | BL | DP | ABY | ACR | Dmoz | C | N | Q | B | Reg | RDT |
|---|---|---|---|---|---|---|---|---|---|---|---|
| esolo.top | 0 | 0 | 2021 | 1 | - | ** | ** | ** | ** | 12 | 10 K |
| bhc331.top | 0 | 0 | - | - | 0 | - | ** | ** | ** | 0 | - |
| bananad.top | 2 | 0 | - | 0 | - | - | ** | ** | ** | 4 | 226 |

Next, compare those results to the following, which I found by sorting by each category. Personally, I like "Rental-Bus.com" and "PrairieBoard.com". Either should pass as a legitimate company name. "PrairieBoard.com" could be presented as a board of directors' entity acting on behalf of practically any business. This may seem overkill for a computer, but I believe it is justified. After purchase, I reserve email addresses associated with this domain solely for use with my new Linux device. When we get into VoIP providers, you will be glad you were proactive with this.

| Domain | BL | DP | ABY | ACR | Dmoz | C | N | Q | Reg | RDT | Status |
|---|---|---|---|---|---|---|---|---|---|---|---|
| PrairieBoard.com | 0 | 0 | - | 0 | ** | ** | ** | 0 | 1 | 2 days | available |
| neamemories.com | 0 | 0 | - | 0 | ** | ** | ** | 0 | 0 | Yesterday 19:44 | available |
| FishyChat.com | 0 | 0 | - | 0 | ** | ** | ** | 0 | 0 | Yesterday 19:45 | available |
| BankerSkit.com | 0 | 0 | - | 0 | ** | ** | ** | 0 | 0 | Today 19:04 | available |
| Rental-Bus.com | 0 | 0 | - | 0 | ** | ** | ** | 2 | 2 | 3 days | available |
| bialdi.com | 0 | 0 | - | 0 | ** | ** | ** | 0 | 2 | 7 days | available |
| polisick.com | 163 | 2 | - | 0 | ** | ** | ** | 0 | 0 | Yesterday 19:43 | available |
| GoodStuffForGoodPeople.com | 0 | 0 | - | 0 | ** | ** | ** | 0 | 0 | Yesterday 19:42 | available |

Next, I like to verify domain registration history through online services such as Whoisology.com. Many online services, especially VoIP providers, can replicate this type of search, so I want to know what they will see if their systems scrutinize a domain associated with a new account. Below is the entry for rental-bus.com. You can see that domain registration has been captured since April of 2013. If I were to purchase this dropped domain and use it with the email account I provide during purchase, I may appear much more legitimate than using a new domain which has never appeared online before.
