
## Nephology

> > I saw a city in the clouds. - Dagobahnian proverb

## Introduction to Cloud Computing

Nephology is the study of clouds. Few modern technology concepts (other than maybe data science and artificial intelligence) have been hyped as loudly as “the cloud.” The cloud is simply a computer which we can access over the internet. In this chapter we’ll set up a cloud computer and we’ll learn the basics of interacting with one.

To get the most out of this chapter you’re going to need your credit or debit card, or a PayPal account. We’re going to be using DigitalOcean, a company which we can rent cloud computers from. Throughout this chapter I might refer to cloud computers as servers (computers connected to the internet) or as droplets, which is a marketing term DigitalOcean uses to refer to their servers (a droplet is not a technical term). Renting from DigitalOcean won’t cost you any money since I’m giving you a coupon for two free months of service! There are several companies that offer similar services compared to DigitalOcean, but in my opinion they have the best user interface and the most transparent pricing model.

33 https://www.paypal.com
34 https://m.do.co/c/53d0d6ef2b37

Check your email for a message from DigitalOcean and click the enclosed link to confirm your email. Then you'll need to enter your credit or debit card information, or your Paypal account details. As long as you close down all of your servers less than two months after you start them you will not be charged. After entering in your payment information you should see this screen:

![](img/a67f2d2ba01c2569ec78ab34ae6c3c5a_217_0.png)

Click the big blue Create a new Droplet button which should then bring you to a screen where you can customize the server you're going to be renting. Make sure you have Ubuntu chosen as your distribution, and select the $5 per month size option:

## Nephology

![](img/a67f2d2ba01c2569ec78ab34ae6c3c5a_218_0.png)

Scroll down the page and then select the region that is geographically closest to you. Some regions have multiple data centers, it doesn’t matter which data center you pick. Currently I’m in Baltimore, Maryland, USA, so I’m going to pick the number 1 data center in New York:

![](img/a67f2d2ba01c2569ec78ab34ae6c3c5a_218_1.png)

Finally at the bottom of the page click the big green **Create** button in order to start your server!

![](img/a67f2d2ba01c2569ec78ab34ae6c3c5a_219_0.png)

It will take a minute to launch the server, but once launched you should receive an email from Digital Ocean with the details about your new server. Included in this email you should find the IP address of your server, the default username (which should be root) and a randomly generated password that you will need to connect to your server for the first time. Once you’ve received this email open up a new terminal.

## Connecting to the Cloud

We can connect to computers on the internet with the ssh program, which stands for Secure Shell. The ssh command provides a command line interface to whichever computer we point it to. A computer that is connected to the internet has an address (just like a house has an address) which is specified by an IP address. The command for connecting to a computer with ssh generally looks like this:

```
ssh [username]@[IP address]
```

Let’s connect to our DigitalOcean server using ssh. Enter the following command in the terminal substituting the IP address you received from DigitalOcean for the IP address I’m using in this example:

```
ssh root@159.203.134.88
```

```
## The authenticity of host '159.203.134.88 (159.203.134.88)' can't be established.
## ECDSA key fingerprint is SHA256:UhtoIx/3c6/MmAIE+H8wSoE06PsbXdzRrSAUhKtJhs.
## Are you sure you want to continue connecting (yes/no)?
```

Type yes and then press Enter.

```
## Warning: Permanently added '159.203.134.88' (ECDSA) to the list of known hosts.
## root@159.203.134.88's password:
```

This password should be in the email you received from DigitalOcean. Copy and paste the password into the terminal, then press Enter.

```
## You are required to change your password immediately (root enforced)
## Welcome to Ubuntu 16.04.2 LTS (GNU/Linux 4.4.0-78-generic x86_64)
##
##   * Documentation:  https://help.ubuntu.com
##   * Management:    https://landscape.canonical.com
##   * Support:       https://ubuntu.com/advantage
##
##   Get cloud support with Ubuntu Advantage Cloud Guest:
```
