**Footprinting** is the process of accumulating preliminary data about a target using publicly available methods. This information can be used to gain a better understanding of the target’s network architecture. This first chapter covers different ways and techniques of gathering such information, including the use of search engines and of domain and network block registrars. Through the least glamorous aspect of hacking methodology, the process of footprinting is an important first step.

# SEARCH ENGINES

Search engines can be used to find interesting details and links that may lead to sensitive information. Since queries are performed on the search engine’s database, they are not noticeable in the target web server’s logs unless a resulting URL is accessed directly.

There exist many ways to perform creative queries for sensitive data. The sections that follow offer a few ideas.

# ### Searching Job Postings for Administrative Weaknesses

A lot of firms advertise available job positions, which can provide a wealth of information about their security posture. For example, if a company is actively recruiting firewall specialists, their firewall configurations may be weak, and this fact provides a hacker with more direction on where to focus. Résumé services such as http://www.monster.com/ are places where potential intruders are known to look for such information.

# ### Searching EDGAR

The EDGAR ("Electronic Data Gathering, Analysis, and Retrieval") database contains information about publicly traded companies. Details such as company acquisitions are of special interest, since large organizations tend to have trouble managing their network security during the initial phase of a merger. The EDGAR database can also be used by potential intruders to gather the target organization’s quarterly and yearly reports, which may help a potential intruder gain a better understanding of the organization’s recent activities. The EDGAR system is located at http://www.sec.gov/edgar.shtml.