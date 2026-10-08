
crack all your DES-based passwords in two days, it might take 40 days to crack your MD5 passwords if he could even get them; he will probably go someone else instead. MD5 allows an unlimited number of significant characters in the password, giving your users more flexibility in choosing passwords.

Shadowed MD5 passwords are much harder to crack than nonshadowed or DES passwords; it is important to convert to shadowed MD5 passwords for good security.

### 2.4.2 Reprompting for the Password

The only things worse than an interloper taking over a user's account is being allowed to "keep it" for a long time. This is the reason that the password prompt prompts for a user's old password before accepting the requester's new password.

Thus, if it is an interloper trying to change the password (while the user has taken a walk) he will be unable to access until the user comes back or the terminal is locked for inactivity. The inactivity timer should be short, typically 2–10 minutes. Another technique for X-based programs is to make use of X's Secure keyboard feature that a program might use to ensure that it has exclusive access to read the keyboard while the user is keying confidential data, such as passwords and credit card numbers. (Certainly, the interloper could create a set-UID shell but he would not be able to access it without first getting "on" the system via another account.)

This limits the interloper's access to a short time. Why should you choose? It is important to understand this reason for prompting for the password even though the "user" is already logged in.

Passwords are requested by Web servers and ordinary application programs. If some sneaks onto your terminal and orders CDs with the latest tunes, they will end up shipped to your address, and e-mail notification (to stop the order) will be sent to your e-mail account. The interloper may be able to delete your e-mail but probably does not have a key to your apartment and so you will be able to return the merchandise for a credit.

The security-conscious Web site will ask that you enter your password into the form used for changing or accessing critical user data such as shipping or billing addresses, credit card numbers, e-mail addresses, or phone numbers. They will use https to protect all confidential data, especially passwords and credit card numbers. Make sure that your browser is indicating that SSL is being used. Recent versions of Netscape 4.* show a closed padlock to indicate this.

I used a site last night that went through all of the trouble of having me connect through hoops to set up my account and pick my password. When I ordered merchandise I noticed that it was using http, not https, to accept my password. Thus, this second time my password was transmitted in clear text, available for the sniffing. We should really have known better. I am choosing not to mention the site because it is a nonprofit organization that does work.

These sites also should e-mail notification saying which items have changed, for example, "We changed your credit card number at your request," without actually including the new credit card number in the e-mail in case someone reads the e-mail, possibly by sniffing. If the e-mail address is changed, notification including the new e-mail address should be sent to the old e-mail address too.

Most financial institutions and investment firms follow a similar procedure postal addresses. They will send a letter to the old address announcing that the address of record has been changed to the new address. If the letter is returned as undeliverable, the address change is probably legitimate. If the firm receives a surprised or angry letter from the investor, theft may have been prevented.

This is to prevent a criminal from first changing an account's address to the criminal's post office box and then proceeding to close the account with a check sent to this new address. The owner might not notice this theft for months because he never sees this statement and does not miss it among the normal deluge of mail.

You will want to ensure that your Web applications follow these good practices. You may not want to do business with Web sites that do not use https to protect confidential data or do other boneheaded things to compromise your credit card. Remember, you will be the one that must hassle with your credit card if a fraud is perpetrated, not the Web site.

In many applications the customer service people must "log in" to the application after logging in their Linux account. This application account and password frequently is independent from the Linux account and a particular application account may be started from any Linux account. It is imperative that whatever application procedure be used for changing the application password and other critical information as you considered for Web sites and changing the Linux password.

### 2.4.3 Should Passwords Be Aged?

Many SysAdmins get a false sense of security by forcing the users to change their passwords (password aging) regularly. A well-picked password could be used for years because a user can remember it and not need to write it down. Forcing a user to give up a well-chosen password can be demoralizing and cause a user deliberately to pick a less secure more easily guessed password. Forcing users to think up subsequent passwords every 12 months will, with each iteration, typically cause less secure passwords to be used and the increasing likelihood that they be written down in an insecure place.

Special note: When passwords be changed, do not e-mail the new to the intruder. If an account is compromised this would give the new password to the intruder. If the intruder had been in other means than the old password, you just gave an additional path in. For an entertaining account of this see "Confessions of a Berkeley System Model" on page 551.

What are the disadvantages of using the same passwords indefinitely?

- A cracker might discover someone's password, especially root's, and lie quiet in wait for months or years and then strike at a most inopportune time.
- Users will tend to use the same password everywhere. Thus, if the password is compromised on one system, possibly by sniffing or a Trojan in login, telnet, or ssh, all the user's systems will be at risk.

With many people having systems at home and cable modems and DSL becoming popular, expect your users' home systems to become compromised. These compromised systems probably contain enough information about the office systems to allow the cracker to penetrate the office systems.

At some companies the root password is not changed even when someone who leaves the company. Be sure to change any password that a departing employee or consultant knows, regardless of how amicable the departure is.

> When I have left some consulting assignments, I have had to plead with the system administrators to change any password that I know. This is not just for proper security. Additionally, it protects my reputation if there is a security breach later.

### 2.4.4 Account Names

You have just examined issues with passwords. However, before a cracker can “crack” a password needs to know the name of an account. It is much more difficult to guess both an account name and a password at the same time than it is to guess the password for a known account. This is why on Linux and UNIX if you enter the account name correct but enter the wrong password, the error message is exactly the same as if the account name does not exist. This is true for the login, telnetd, and ftpd programs. Thus, they will not allow a cracker to discover which account names are valid.

The truly cautious might want to have e-mail names not correspond with account names. This would be overkill for some. However, it could be done by editing the /etc/aliases file to map e-mail addresses as sales to the actual account name for incoming e-mail. For outgoing mail, the generic can be used to map the actual account back to the externally visible e-mail address, such as "sales." This could be done for individual accounts too. Thus, Sam Spade might have e-mail at ssp@pentacorp.com and have account on shoe.pentacorp.com.

For additional security, many sites use separate systems for services. Typically e-mail, Netscape, and Usenet clients would be on one set of systems, the Web server and related operations on another, internal accounting and operations on others. The cost per megabyte and per computer is so low that this is very practical. (A computer is a term meaning unit of computation in a computer. I cannot recall what engineer I first heard using the term; I believe that was at Stratus Computer.

This is addressed in several other chapters including "Intracomunity Firewalls to Contain Fires" on page 78, and "We Fall, Divided We Stand" on page 109.

Some installations already have the host name for all e-mail addresses be that of the domain, for example,

```
sales@pentacorp.com
```

This makes it easy to move people's accounts between actual systems without the difficulty of everyone needing to update their e-mail addresses.

# Protecting the System from User Mistakes

![](img/7d04225c75a86d3cf4bd6077596f35b2_66_0.png)

There are many more users than SysAdmins, all are less knowledgeable security, and most are too busy doing their job to worry about security. This is a good reason to take steps to protect the system and network from the users. (You are really protecting the company's assets and reputation.) The level of trust given to users to vary greatly depending on the circumstances and fairly deciding that level while sufficiently protecting the organization's system without becoming Draconian is a lofty goal that is to achieve. It is harder than getting the right amount of food and drink for a party.
