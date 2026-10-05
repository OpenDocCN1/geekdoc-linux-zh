
# OffSec

Penetration Testing with Kali Linux attack included financial losses for specific Twitter users, data exposure for a number of high-profile accounts, and reputational damage to Twitter itself.

To understand potential prevention and mitigation, we need to understand how and why the attack occurred. The attack began with spearphishing and social engineering which allowed attackers to obtain employee credentials and access to Twitter's internal network. This could have been prevented if employees were better equipped to recognize social engineering and spearphishing attacks. Additional protections that could have prevented or mitigated this attack include limiting access to sensitive internal tools using the principle of least privilege and increased monitoring for anomalous activity.

**Phishing.** Phishing is a general class of attack relative to spearphishing. Spearphishing attacks are targeted to specific individuals; phishing is usually done in broad sweeps. Phishing strategy is to send a malicious communication to as many people as possible, increasing the likelihood of a victim clicking a link or doing something that would compromise security.

In September 2021, a subsidiary of Toyota acknowledged that they had fallen prey to a Business Email Compromise (BEC) phishing scam. The scam resulted in the transfer of ¥ 4 million (JPY), roughly to 37 million USD, to the attacker. This attack occurred because an employee was persuaded to change account information associated with a series of payments.

The United States Federal Bureau of Investigation (FBI) recommends these and other steps to prevent BEC:

- Verify the legitimacy of any request for payment, purchase or changes to account information or payment policies in person.
- If this is not possible, verify legitimacy over the phone.
- Be wary of requests that indicate urgency.
- Carefully inspect email addresses and URLs in email communications.
- Do not open email attachments from people that you do not know.
- Carefully inspect the email address of the sender before responding.

**Ransomware.** Ransomware is a type of malware that infects computer systems and locks a legitimate user from accessing it. Users are often caught by the attacker and asked for a ransom in order to unlock their machines or documents.

In May 2021, a ransomware incident occurred at Colonial Pipeline, a major American company. The attack led to the disruption of fuel distribution for multiple days. This attack resulted in a loss of corporate data, the halting of fuel distribution, millions of dollars in ransomware payments, increased fuel prices, and fuel shortage fears.

> 46 (Forbes, 2019), https://www.forbes.com/sites/leatmathews/2019/09/06/toyota-pays-supplier-hit-by-37-million-email-scam?ish=30c5da85
> 47 (FBI, 2021), https://www.fbi.gov/scams-and-safety/common-scams-and-crimes/business-email-compromise
> 48 (ZDNet, 2021), https://www.zdnet.com/article/colonial-pipeline-ransomware-attack-everything-you-need-to-know/

# OffSec Penetration Testing with Kali Linux

In this attack, hackers gained access to Colonial Pipeline's network with a single compromised password. This attack could have been prevented⁴⁹ or at least less likely by ensuring that MFA was enabled on all internet-facing resources, as well as prohibiting password reuse.

**Credential Abuse**: Credential Abuse can occur when an attacker acquires legitimate credentials, allowing them to log into machines or services that otherwise would not be able to. Often, attackers are able to guess user passwords because they are predictable or weak.

In December 2020, many malicious updates were discovered in the SolarWinds Orion platform, an infrastructure monitoring and management tool. These malicious updates allowed malware to be installed on the environment of all SolarWinds customers that installed this update and led to the compromise of a number of these customers, including universities, US government agencies, and other major organizations.

As a supply-chain attack, this affected approximately 18,000 SolarWinds customers and led to the breach of a subset of customers including government agencies and other major companies. According to SolarWinds CEO Kevin Thompson, this attack resulted from a weak password⁶¹ that was accidentally exposed on Github. This attack could have been prevented⁵² by ensuring that passwords are sufficiently strong and by monitoring the internet for leaked secrets. CISA has also stated that this attack could have been mitigated by blocking outbound internet traffic from SolarWinds Orion servers.

**Authentication Bypass**: While Credential Abuse allows attackers to log in by legitimate authentication, Authentication Bypass allows attackers to ignore or step-around authentication protocols.

Similar to the SolarWinds attack, on July 2021⁵³ an attack was detected that took advantage of a vulnerability in software vendor Kaseya's VSA remote management tool. Attackers were able to bypass the authentication of the remote tool to eventually push REvil ransomware from compromised customer Virtual System Administrator (VSA) to servers via a multiple attack.

Since this attack targeted a number of Managed Service Providers (MSPs), its potential scope encompassed not only the MSP customers of Kaseya, but also the customers of those MSPs. According to Brian Krebs⁵⁴ this vulnerability had been known for at least three months before this incident. This attack could have been prevented by prioritizing and fixing known vulnerabilities in an urgent and timely manner.

## 3.3 The CIA triad

This Learning Unit covers the following Learning Objectives:

- Understand why it's important to protect the confidentiality of information

> 49 (CISA, 2022), https://www.cisa.gov/stopransomware/how-i-protect-against-ransomware
> 50 (BBC, 2020), https://www.bbc.com/news/technology-553216423
> 51 (ZDNet, 2021), https://www.zdnet.com/article/colonial-pipeline-ransomware-attack-everything-you-need-to-know/
> 52 (SC Media, 2021), https://www.scmagazine.com/
> 53 (ZDNet, 2021), https://www.zdnet.com/
> 54 (Krebs, 2021), https://krebssecurity.com/
