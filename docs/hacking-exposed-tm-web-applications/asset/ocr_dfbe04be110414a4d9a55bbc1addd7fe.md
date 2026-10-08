# Appendix D: UrlScan Installation and Configuration

+   - Install the UrlScan filter, including updates.
- Edit the UrlScan.ini configuration file according to your needs, necessary.
- Restart IIS.

(The last three steps can be performed automatically using the IISLockdown tool.) We will discuss each of these steps in detail in this appendix. We have divided our discussion into basic and advanced levels. For those who fire and security without bothering to understand what UrlScan is doing, read the section "Basic UrlScan Deployment" later in this chapter. If you are hands-on and want the technical details of how to manually deploy UrlScan and tune it to suit your needs, skip ahead to the section "Advanced UrlScan Deployment."

# OBTAINING URLSCAN

To obtain UrlScan, download the IISLockdown tool from the link listed in the "References and Further Reading" section in this appendix. The UrlScan files from the IISLockdown package are version 2.0 of this writing (UrlScan DLL build 6.0.3544.1). In order to update UrlScan to the latest version, you will have to obtain the latest installer as well.

# Updating UrlScan

In 2002, Microsoft published an updated tool called UrlScan.exe that updated installed UrlScan files to the most recent version (replaced UrlScan.dll and made a few entries to UrlScan.ini). As of this writing, the most recent version of UrlScan is 2.5 (build 6.0.3615.0).

To confuse matters, there are actually two versions of the urlscan.exe updater: Baseline UrlScan and UrlScan-SRP. watch out! The main difference between Baseline and SRP lies in some minor configuration changes introduced into the IISini file (the UrlScan filter itself is exactly the same between Baseline and SRP). SRP's configuration blocks so-called "chunked encoding" of HTTP transfers, which lie at the root of server vulnerabilities in IIS 5.x around of Microsoft in April. In addition, uploads to the server are restricted to 30MB in SRP configuration (it is 2GB in Baseline). Other than these configuration differences (which can be manually changed), Baseline and SRP are identical. We recommend using SRP unless you know you will have to service clients that rely on chunked encoding.

A link to the 2.5 upgraders is provided in the "References and Further Reading" section later in this appendix. At this point, we will assume that the necessary files have been obtained, and will discuss UrlScan deployment. But before we do, let's cover one important item not addressed by UrlScan: updating Windows.