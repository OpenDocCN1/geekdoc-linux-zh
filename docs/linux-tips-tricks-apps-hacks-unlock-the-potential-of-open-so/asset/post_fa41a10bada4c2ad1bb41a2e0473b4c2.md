
# PASSWORD SECURITY

Creating an invincible password is the first step to securing everything.

One of the most important steps in keeping anything secure is to create a very strong password that is difficult to crack. While movies will tell you enterprising hackers just need to look around your office to figure out your password ('it's his son's name - easy'), the most common method of password cracking is the brute force attack on the server and the username. Under a brute force attack, short passwords, unmodified dictionary words and anything on top password lists will succumb very quickly. In terms of length of password versus time to crack it, the hours and days needed to successfully discover a password are always going down thanks to advancements in CPU speed and bandwidth. Using simple alphanumeric passwords are increasingly insecure, even if they're as long as ten characters. Let's start with a password then and modify it - a non-dictionary word, reasonably long. Plucked out of the air we have:

```
dwanton
```

— Seven characters, lower case letters

**Time to crack: two seconds**

Seven is quite short. If you're using it online, most websites require a minimum of eight letters, a capital letter and a number. This drastically improves the quality of the password, both offline and online. A basic modification would be:

```
Dwanton1
```

— Eight characters, alphanumeric mixture of lower and upper case

## How secure is my password?

![](img/30dc0459712b32ede1a3814d456b41b6_102_0.png)

*Above: There are a few websites that will check your password, but make sure to use something similar*

**Time to crack: 15 hours**

Doing a lot better! The password is immediately exponentially more secure, although 15 hours is still not that long. We can do better by adding a symbol to the mix in an easy-to-remember location:

```
Dw@nton1
```

— Eight characters, alphanumeric and symbol mixture

**Time to crack: 3 days**

Another big jump to three days. In theory, most people would give up by now, but as we're dealing with an automated brute force, that won't matter. We're at about as secure as we can be with an eight-character password in terms of brute force, and the '1' at the end is a bit basic. By just making it a two digit number we can further increase the time to crack:

```
Dw@nton12
```

— Nine characters, alphanumeric and symbol mixture

**Time to crack: 275 days**

275 days is a quite a while, but it's still doable for persistent crackers. Adding a symbol, letter or number to the end of this password will increase its lifespan to 58 years. 58 years is a massively long time for someone to be trying to crack your password without upgrading their hardware and software or simply forgetting about it. So here's an example of an excellent starter password idea:

```
Dw@nton12*
```

We say starter, as while this is an excellent password, you shouldn't be using it on every account that you have. If a list of passwords is leaked due to someone else's insecurity, it doesn't matter how long your password will take to brute-force if they already know what it is. If you hear of a leak, change your password immediately.

> “Using simple alphanumeric passwords is becoming increasingly insecure”

## PASSWORD DO'S & DON'TS

- **DO**
  - Use capitals, numbers and basic symbols
  - Reset online ones every six months
  - Make sure it's at least nine characters long
  - Run something similar to your password through a password checker
- **DON'T**
  - Use dictionary words
  - Use phrases
  - Use personal information
  - Use consecutive numbers
  - Use numbers such as your two-digit birth year
  - Use the same password everywhere
  - Write them down
  - Make them too long

# ONLINE SECURITY

Effectively use your passwords online and employ other security measures.

Now we have a basic password, it’s time to start implementing it online. Security experts say you should use a different password for every account. Services like LastPass can offer a convenient way of doing this with truly unique passwords per account, but you might not be comfortable with them. Human beings can only remember so many passwords; as you most definitely should not be making a note of these passwords, what we suggest is to modify the password based on what website you’re using it on.

For example, let’s take Amazon. It has your credit card details so securing the account is extremely important. After the ‘Dw@en’ of the ‘dwaonton’ base we have three characters to play with, so we could change them for our Amazon password. Here’s our working: Take the middle three letters of the site’s name (As Amazon is six letters long we will choose ‘maz’), and reverse the letters to ‘zam’. Now insert it into our password:

```
Dw@nzam12*
```

This still has the high level of security, but will be different from, say, eBay (Dw@nab1e12*) or Github (Dw@nhgb12*), without being immediately obvious to whatever cracking program would then try and use that password on other websites and accounts. A smart enough human might crack the code, but this is only an example of how you can modify your password while still making it memorable to yourself.

## Security and Privacy

Last issue we touched upon how to keep your details as private as possible. As well as brute force attacks, crackers can perform confidence and social manipulation tricks with phone support to deceive you, using any information they can gather from social accounts. Some of the privacy-oriented recommendations can help keep angles of attack secret from malicious people.

Go through your social media accounts – Twitter and Facebook mainly – and look at your privacy settings. Make sure nothing sensitive is set to private, and even think of removing terms that you don’t need on your profile, such as phone numbers on Facebook or location on Twitter. Most importantly, keep your main email address completely secret: never share it on Twitter unless via a DM to someone you trust and don’t keep it in your profile. For work email, use a different address and link as few accounts as possible to that email.

Lastly, while an extreme step, you can always look at not using your real name on your more public social media accounts. Facebook won’t truly allow it for personal accounts, but everywhere else you can it’s a good idea to use a pseudonym if you want to be as secure and private as possible.

![](img/30dc0459712b32ede1a3814d456b41b6_103_0.png)

**Above** LastPass won our password managers group test a couple of issues back
**Below** Controlling your visibility on platforms like Facebook is crucial to security

## TWO-FACTOR AUTHENTICATION

One of the best security features of the recent years is two-factor authentication. Google, Apple, Tumblr and many other services and websites now include two-factor authentication to increase security. Usually, a mobile number is securely supplied to the company, which then sends you a message, including a special, one-use code to work in conjunction with any system you’re trying to log into the account with. Other companies will send it via email or allow you to use a special app similar to banking keypads. Turning this on may be slightly inconvenient to some, but the peace of mind and added security is well worth it.

![](img/30dc0459712b32ede1a3814d456b41b6_103_1.png)

# NETWORK SECURITY

Protect your local network from the occurrence of external or local intrusions.

![](img/30dc0459712b32ede1a3814d456b41b6_104_0.png)

Below some tools may be superfluous depending on how you use your system. Left Changing settings in the router can really improve your network’s security

![](img/30dc0459712b32ede1a3814d456b41b6_104_1.png)

Now you’ve secured your online life, it’s a good idea to look at your actual physical network of home or office PCs, laptops and other devices. Having a strong password on your GMail account is one thing, but if someone can see exactly the kind of packets are going back and forth they can likely figure out what you’re looking at. Securing your network is an important step, but it’s also fraught with problems you may never know exist, especially when you try to balance convenience with security on a system provided by an ISP.

Shared folders, Samba servers and SSH access are very common within networks, allowing you access files and folders remotely. They’re also excellent attack vectors by those who can get into your network. Uninstalling or deactivating networking services you don’t use is a great way to increase security throughout your network. This is another convenience versus security debate – some networked devices (such as a Raspberry Pi or file server) you may wish to SSH into. That’s fine, just make sure that to access them, you require a strong password. Same with the Samba shares for distributing music over your home network and the like. VNC can probably turn off and on via SSH so you only access it when you definitely need to. There’s a lot of just thinking about how you interact with other devices over the network in terms of network security that can help out.

## Network monitoring

What if there’s activity over your network that you don’t know of and therefore can’t immediately fix? One of the best tools in any sysadmin or network security toolbox is Wireshark, or more specifically, the tshark command line implementation.

## FIREWALLS

Your router will come with a firewall built in and it will be pretty good. If you have a custom server on your network, either at home or around the office, then you can probably make a better one – one that you have far more control over and that will do a better job of protecting your network overall.

You can do this simply by using “iptables”, a command-line tool available for any version of Linux that lets you set up custom rules for IP addresses that can access the server; custom port forwarding and other little changes that make it a lot more useful to certain people.

The Arch and Ubuntu wikis have some great guides: bit.ly/yCwW4K (Arch) and bit.ly/1gc18tu (Ubuntu).

## Router maintenance

Your router, as the creator and guardian of your network, isn’t impervious to attacks either. As well as updating any default passwords that may exist for the admin user, you should always make sure to update your router’s firmware as regularly as possible. Updates will include security fixes for any vulnerabilities that are present and should improve security across the router’s software overall.

If your router allows it, you can also attempt to change the default IP addresses and range. If you’re using DHCP, this won’t matter to any connected devices, but changing the default network addresses from the common 192.168.x.x structure will stop other types of attacks on the network that specifically target the router.
