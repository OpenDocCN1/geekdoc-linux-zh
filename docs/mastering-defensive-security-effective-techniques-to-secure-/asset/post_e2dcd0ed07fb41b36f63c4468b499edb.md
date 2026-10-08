
# 18 A Refresher on Defensive Security Concepts

Here, the attacker gathers email/password combinations from published password breaches and uses them to trick people into believing that they have been hacked for a long time and that the hacker contains sensitive information about the person. There are several variants of these attacks that vary from telling the victim that the hacker accessed the webcam and have compromised videos/photos of the victim, or that the hacker has access to the browsing history and it will publish the victim’s "dirty" website history unless payment is made.

![](img/8c6a223c57e25ea0cc1593903a1b920f_40_0.png)

Hey I know your pass is: "my old password on a password leak"
I infected you with my private malware (RAT) (Remote Administration Tool), a few months back when you visited some website where my iframe was placed and since then, I have been observing your actions.
The malware gives me full access and control over your system, I can see everything on your screen when you turn on your camera or microphone and you won't notice anything about.
I have also access to all your contacts, private pictures, videos, everything!
I MADE A VIDEO showing you (your webcam) SATIFYING YOURSELF! You got a very good taste! Hahaha.
I can send this to all your contacts (email, social network) and publish all your private data everywhere!
Only you can prevent me from doing this! To stop me, transfer exactly 1600$ with the current bitcoin (BTC) price to my bitcoin address. It it's a very good price compared to the damage and hell it can bring into your life!
Bye!

Figure 1.7 – Example of a scam email

As a security expert, you may have received an email like this one, but as a professional, your mission is to help others from falling victim to these kinds of attacks, from family and friends to coworkers, and especially high-targets, such as executives of your company. The best way to deal with these kinds of attacks is through education. In fact, user education is one of the keys pillars for any cybersecurity strategy. This topic is so important that I decided to create an entire chapter for you!

> Tip
> Use your social media as a tool to let others know that this is a hoax. Try to post something related to these kinds of attacks on your LinkedIn, Facebook, and Instagram accounts at least every months. This simple act may save you a lot of trouble and money while helping you to grow your social eminence.

As a cybersecurity expert, you have great powers, but also great responsibilities.

# Brute-force attacks

One of the most common attacks on passwords is brute-force attacks. By far the most famous app to achieve this is John the reaper, in which you can customize the attack to reduce the time required to expose a password.

In these types of attacks, password complexity (and size) matters, so let me use some math to prove it.

We have two variables: the spectrum of possibilities (S) and the password length (L). In the alphabet, we have 26 characters, so it means our spectrum of possibilities is 26, but that is considering just one case, because if we use lowercase and uppercase, then it increases to 26+26=52.

This means if we have an 8-character password (L) with just lowercase letters (S), the number of possibilities will be SL^L, or in this case, 26^8, which means around 200 billion combinations.

Some of you may think that 200 billion is a huge number of possibilities to guess, but a modern computer can guess 100 billion combinations every second, which means our 8-character password with just lowercase can be cracked in 2 seconds.

But no worries, all we have to do is to increase the spectrum of possibilities (S) as follows:

- By adding numbers, the spectrum (S) increases by 10. This is equal to 36^8, which can be guessed in 30 seconds.
- By adding special characters as well, the spectrum (S) increases by 32. This is equal to 64^8, which can be guessed in 1.5 hours.
- By adding uppercase, too, the spectrum (S) increases by 26. This is equal to 94^8, which can be guessed in 20 hours.

All this proves that an 8-character password is no longer secure. Therefore, to be considered secure, a password should be at least 10 characters long and include all of the above. This math is very important, especially to support the requirements to determine the password policy of your organization (and gain the buy-in from users and executives).

> Tip
> you want to check the password strength without having to do all the math, I recommend the following site: https://www.grc.com/haystack.htm

# Dictionary attacks

This is similar to a brute-force attack, but instead of guessing the password, it uses a dictionary with the most common passwords.

You can find dictionaries with millions of passwords. In fact, some of them are so big that they can make Notepad crash. So, to make it easier for the attacker, most dictionaries are sorted by topic, region, length, or by source (normally from a password breach).

As mentioned, this attack is different from the attacker's point of view, but the same tips provided earlier work for this type of attack.

If you want to see what dictionaries look like, here you can see many dictionaries sorted by various factors: http://www.md5this.com/tools/wordlists.html.

> Test yourself
> Take a look at these two passwords and think which one is more secure, and then go to the link above and see the results:
> LoL********
> C4b-6W@#5

# Creating a secure password

If there has ever been a never-ending debate, it is probably the one about password strength. My grandpa used to say: Avoid talking about religion, politics, and soccer because it will always end in a fight and you will lose many friends. Well, I think that "password strength" conversations should also be included on that list.

I remember being on a board of experts from all around the world discussing very challenging topics and, despite our differences, we were able to agree on all topics but one: passwords!

Some experts believe in pure length (such as long phrases), others in complexity (they want something unreadable), others want both, but the most controversial topic is around password expiration. There are many two parties – the dictatorial and the user friendly.

The dictatorial does not care about the user experience, they just want to create the rules and leave it up to the user to figure out how to comply (even if this means writing the password on a sticky note).

# Managing cybersecurity's legendary point: Passwords

On the other hand, the user-friendly group uses a more empathetic approach by analyzing how realistic it would be for users to comply.

In context, instead of taking one side or the other, you must make your decisions based on facts (data never lies). Therefore, to create a bullet password expiration policy, I recommend that you find a response to the following questions:

- How technical is my audience?
- How educated are they in terms of passwords?
- Can you apply segmentation based on user roles? (Privileged users will change their password every 90 days, while regular users will do this every 180 days).
- Do I have the infrastructure to enforce this policy?
- Can you apply segmentation based on the data/systems accessed/used?
- Do they have the tools and training to create/manage complex passwords?

Additionally, there are Three Golden Rules to improve your password security within your organization:

1. Implement password vaults: By default, people don't trust putting all your credentials on an app. In this case, you need to educate users and show them all the benefits of using a password vault (starting with the fact that this is better than having the password on a post-it under your keyboard).

But don't go the hard way by making a policy and forcing everyone to implement it. Instead, lead by example, show the people how much you love using your password vault, how easy it is to use, and how convenient it is to log on all your apps with a single click. Brag about how you have a unique bullet proof 80-character password for each of your accounts, a different password for each account. Let them know that this is not just for corporate usage, but for personal life. The only thing you need is a password vault app (there are many free and open source options) and a master password to unlock it (since you only need to remember one, make sure this one is secure). Remember that passphrases are always a good option.
