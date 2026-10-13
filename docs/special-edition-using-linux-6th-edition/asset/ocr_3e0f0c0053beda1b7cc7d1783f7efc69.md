# # What Is BIND?

Several different DNS servers are available under different names. The most common, and the one you’ll find on your Linux system, is the Berkeley Internet Nameserver Daemon (BIND). As of this writing, the current major version number is 8.

# ## About Domains

Before you go further, it is helpful to understand a little about domains. You’ve seen domain names before. They are in the form of bar.org, and contain at least two parts. Reading from the right, the org part is called a *top-level domain*. A number of top-level domains exist. In the United States, currently, are the following top-level domains:

+   - `.com`—Commercial entities (businesses)
+   - `.org`—Non-commercial organizations
+   - `.net`—Network affiliated organizations
+   - `.mil`—U.S. military branches
+   - `.gov`—U.S. government agencies
+   - `.edu`—Educational institutions
+   - `.int`—International organizations
+   - `.us`—The U.S. domain, which has each state as lower-level divisions

Additional top-level domains have been proposed, but have not yet been implemented.

In other countries, top-level domains are administered by the Internet authorities of those countries and include a two-letter country suffix. Some examples are as follows:

+   - `.uk`—United Kingdom
+   - `.ca`—Canada
+   - `.mx`—Mexico
+   - `.za`—Zud Africa (South Africa)

Within each of the countries, a top-level domain structure, which is decided by the country’s Internet authority, exists. These might or might not correspond to the top-level domains found in the U.S.

Below the top-level domain is the name of the institution or organization that constitutes the actual domain name. For example, ibm.com, or ibm.co.uk. These examples are IBM’s domain names in the United States and the United Kingdom, respectively.

Some large domains also have *subdomains*. Very large institutions might have subdomains. For example, the army.mil domain, which has military bases all over the world and which has very large units on those bases, might be further broken down into subdomains. Therefore, a large base such as Fort Bragg, North Carolina, will have a subdomain ftbragg.army.mil. Because