![](bbox=[0.16, 0.13, 0.85, 0.39])

Figure 23. Searching with a Filetype Operator

We only get one result but it is an interesting one. Our query found the login page for an instance of AlienVault OSSIM,145 a security information and event management (SIEM) platform. Security teams use SIEM tools to monitor applications and network traffic for malicious activities. Usually these tools are only available on internal networks. We should note this URL as it might prove useful if we can find user credentials to login during the active exploitation phase.

The ext operator could also be helpful to discern what programming languages might be used on a web site. Searches like ext:jsp, ext:cfn, ext:pl will find indexed Java Server Pages, Coldfusion, and Perl pages respectively.

We can also modify an operator using - to exclude particular items from a search, narrowing the results.

For example, to find interesting, non-HTML pages, we can use site:megacorpone.com to limit the search to megacorpone.com and subdomains, followed by -filetype:html to exclude HTML pages from the results:

145 (AT&T, 2019), https://cybersecurity.att.com/products/ossim