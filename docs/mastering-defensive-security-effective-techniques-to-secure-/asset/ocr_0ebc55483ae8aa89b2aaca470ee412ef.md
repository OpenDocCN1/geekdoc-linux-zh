# Hijacking a user session

Here, the attacker will try to inject malicious code into a web application that can be used to exfiltrate the session cookie that will be used to impersonate the victim.

To illustrate this attack, let's see an example based on a web application used to rent houses, as follows:

+   1. The attacker will log in to the vulnerable site and create an entry to advertise the renting of a house but inside the description of the field (which a normal person will describe the goodies of the house for rent), the attacker will embed malicious code aimed at gathering the user's session cookie and sending it to their server.
2. When another user opens that hacked advertisement to rent a house, the malicious JavaScript will be executed and the victim's session cookie will be copied and sent to the attacker.
3. Now, the attacker can impersonate the victim by the stolen session cookie to identify themselves as the victim on the system, as shown in the following screenshot:

![](bbox=[0.243, 0.442, 0.756, 0.735])

Now, let's see how you can prevent this attack. You could do the following:

+   * Set php.ini directives, as follows:

```
session.use_only_cookies = 1 -> for using only cookie based session ids
session.use_trans_sid = 0 -> disable showing PHPSESSID in browser url
```