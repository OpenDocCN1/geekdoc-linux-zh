```
<Directory "/ssi">
Options +Include
</Directory>
```

This configuration segment disables the **exec** command everywhere but in the /ssi directory.

# Using SSL for secured transactions

Electronic commerce on the Web is booming at an extraordinary rate. Many companies maintain e-commerce Web sites to conduct business on the Internet. One prerequisite for an e-commerce site is to have secure transaction capabilities, which are provided by Secure Sockets Layer (SSL). Multiple choices for third-party SSL software are currently available for Apache. Table 12-5 should help you pick the right one for your needs.

Table 12-5 SSL Solutions for Apache

| Software | Distribution | Comments |
| :--- | :--- | :--- |
| Apache-SSL | Free | Not recommended, because it isn't the cleanest solution. Apache-SSL is basically a set of patches for Apache and isn't very well documented. |
| mod_ssl | Free | A clean solution. Although partly based on Apache-SSL, it is much cleaner and better documented. Recommended by the author. |
| Rad Hat Secure Server | Commercial | The cheapest commercial solution. Based on the mod_ssl module. |
| Raven SSL module | Commercial | A midrange solution, price-wise. |
| Stronghold Web Server | Commercial | The author's personal favorite SSL solution for serious e-commerce sites. It is the most expensive commercial options. |

The **mod_ssl** module not only is a much cleaner approach than Apache-SSL, it's free. Although it is partly based on Apache-SSL, it is yet another well-documented module by Ralf S. Engelschall. I recommend using this if you are using the latest version of Apache.