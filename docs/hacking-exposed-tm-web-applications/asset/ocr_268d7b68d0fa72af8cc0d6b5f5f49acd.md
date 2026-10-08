# Appendix A: Web Site Security Checklist 313

| Item | Check |
| --- | --- |
| Web Server | |
| Operating system auditing enabled, as well as Web server logging in W3C format | |
| Unnecessary HTTP modules or extensions disabled on all servers (e.g., unused IIS ISAPI DLLs unmapped, Apache mods uninstalled) | |
| Sample Web content / applications removed from all servers | |
| Appropriate authentication mechanisms configured for relevant directories | |
| Secure Sockets Layer (SSL) is deployed to protect traffic that may be vulnerable to eavesdropping (e.g., HTTP Basic Authentication) | |
| Virtual roots containing Web content deployed on a separate, dedicated drive/volume (without administrative utilities) | |
| If possible, account running HTTP service should be low privileged | |
| Appropriate Access Control List set for Web directories and files | |
| WebDAV functionality disabled or if not used; otherwise, WebDAV should be heavily restricted | |
| Web Publisher functionality (for Netscape/iPlanet products) disabled | |
| IISLockdown tool and UrlScan deployed appropriately on Microsoft IIS servers | |
| Servers scanned by vulnerability scanner for remotely exploitable vulnerabilities; issues addressed | |
| For Microsoft servers, use Microsoft Baseline Security Analyzer to analyze the security of the server | |
| Database Server | |
| Database software installed to run with least privilege (e.g., in the context of a low-privileged local or domain account account on Microsoft SQL Servers) | |
| Database software updated to the latest version with appropriate vendor patches | |
| Sample accounts and databases removed from the server | |
| Appropriate IP packet filtering enabled to restrict traffic between Web servers and database servers (e.g., router or IPSec filters on Windows 2000 and above) |