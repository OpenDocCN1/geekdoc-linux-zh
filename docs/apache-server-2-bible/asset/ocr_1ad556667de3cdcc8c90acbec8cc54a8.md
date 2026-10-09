# # CHAPTER 19

# ## Securing Apache with SSL

Only a few years ago, the Internet was still what it was initially meant to be—a worldwide network for scientists and engineers. By virtue of the Web, however, the Internet is now a network for everyone. These days, it seems as though everyone and everything is on the Internet. It is also the new economy frontier; thousands of businesses, large and small, have set up e-commerce sites to open doors to customers around the world. Customers are being cautious, however, because they know that not all parts of Internet are secured.

To eliminate this sense of insecurity in the *new frontier*, Netscape Communications (now a subsidiary of AOL Time Warner) invented a security protocol that ensures secured transactions between the customer’s Web browser and the Web server. Netscape named this protocol as Secured Socket Layer (SSL). Quickly SSL found its place in many other Internet applications such as e-mail, remote access, etc. Because SSL is now part of the foundation of the modern computer security infrastructure, it is important for you to know how to incorporate SSL into your Apache server.

Apache does not ship with any SSL support by default. However, you can compile and install an SSL module for Apache to enable SSL capabilities. There are two open-source solutions available for Apache: `mod_ssl` and Apache-SSL. Both of these solutions use an open-source implementation of SSL called OpenSSL. In this chapter I discuss how you can compile and install OpenSSL and then set up Apache with either `mod_ssl` or Apache-SSL.

# ### Introducing SSL

Using both symmetric and asymmetric encryption schemes (which are described in the "Understanding encryption" section later in this chapter), Netscape developed the open,

# **In This Chapter**

+   - Understanding how SSL works
+   - Setting up OpenSSL
+   - Compiling and installing `mod_ssl` for Apache
+   - Compiling and installing Apache-SSL for Apache
+   - Getting server certificates
+   - Creating a private certificate authority