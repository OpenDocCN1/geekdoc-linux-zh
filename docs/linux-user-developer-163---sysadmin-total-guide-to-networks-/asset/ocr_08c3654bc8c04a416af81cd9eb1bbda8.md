# Secure your web server with Let's Encrypt

# Making up a secure web server easy with this simple way to manage HTTPS

Whether you manage your own Linux server or you're in the process of setting up one for live use or testing and development), there is a strong possibility that you will need to configure HTTPS and SSL certificates. The “secure source” of online shopping, banking and data management is

encryption issue – a problem that can break websites – all advantage in the de-centralization of security-major. Various methods

Currently in SSL certification – highlighted in 2015 with the Superfish malware, and the problems maintaining OpenSSL – it is becoming increasingly difficult to ensure true security. Using Let's Encrypt enables local creation of keys – a major

of acquiring and maintaining certificates, and can be installed easily relatively to your Linux server. Once up and running, you can interact with the Let's Encrypt client in the terminal. Here, you will be able to configure the client based on your requirements, such as adding a HTTP to HTTPS redirect, and revoke certificates as and when.

# 01 Install Let's Encrypt

For the best results, use Debian, with web server already installed and configured. Some distros include letsencrypt package form. Find this first with an update.

```
sudo apt-get-update
```

Then:

```
sudo apt-get install letsencrypt python-apache
```

The python-letsencrypt-auto package is comes if you're not planning to use the Apache plugin. Once installed, you can use letsencrypt to run. You can also install the letsencrypt package from GitHub, but to do that you will first need to install it on your system. Use apt-get install git to do the same commands, or directly from GitHub:

```
git clone https://github.com/letsencrypt/ letsencrypt
```

![](bbox=[0.285, 0.635, 0.77, 0.755])

# Christian Crawley

is a former IT software developer with a quirky personality engineer and since 2010 has been providing inspiration to computer and industry online and in print. Find more at makeof.com.

# Resources

Let's Encrypt letsencrypt.org

Right You can use the Let's Encrypt client to obtain free SSL certificates from the new authority