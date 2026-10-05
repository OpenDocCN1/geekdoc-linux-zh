# Chapter 17 DNS: The Domain Name System

Parent domains should check to be sure that child domain name servers are up and running before performing the delegation. If the servers are not working, a "lame hope" results, and you might receive nasty hope asking you to clean your DNS act. Page 678 covers lame delegations in more detail.

# 17.6 DESIGNING YOUR DNS ENVIRONMENT

Many factors affect the design of a robust and efficient DNS environment: whether the size of your organization, whether you use RFC1918 IP addresses on your local network, whether you use DHCP, whether you Microsoft's Active Directory, whether your internal network is routed or switched, and where your firewall is in relation to your DNS servers, to name a few. You may find it helpful to split the problem into three parts:

+   - Managing the namespace hierarchy: subdomains, multiple levels, etc.
- Serving the authoritative data about your site to the outside world
- Providing name lookups for your users

# Namespace management

If you are site and independent, the use of subdomains is neither necessary nor desirable unless management requires them for sometechnical reason. On the other hand, in a medium-sized organization with several independent systems, subdomains can reduce the need for site-wide coordination. (Subdomains divided along geographic or departmental lines are most common.) A large organization has little hope of enforcing unique names throughout its site and therefore needs subdomains, at multiple levels.

Recent additions to DNS have defined zone-level records (SPF and DKIM/ADSP) to help prevent other sites from forging mail that appears to originate from your domain. Optimal use of these features may require you to define subdomains based on the sensitivity of the information your organization sends by email. See page 591 for more details.

The creation of subdomains requires communication and cooperation between the admins responsible for the parent domain and those responsible for the subdomain. The time subdomain is delegated and set up, be sure to make aware of whom to contact if you want to add, change, or delete servers. Make sure your firewall does not block access to the subdomain's servers if you want the subdomain to be accessible from outside your organization.

If you use subdomains to manage your namespace, run the doc (domain control) tool from cron once a week to be sure that your delegations stay synchronized and that you don't inadvertently create lame delegations. The DNS tools section (see page 667) describes doc and several other tools that help keep DNS healthy.