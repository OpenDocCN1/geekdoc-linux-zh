# CHAPTER 8
# Cracking Linux Passwords

Just as passwords hashes can be hacked in Windows, the same can be done with Linux machines. All you need is root level access to obtain the hashes and a good password attack tool to crack them. In this chapter we will use John the Ripper to try our hand at cracking Linux passwords. We will then cover several other tools that can be used to crack server application passwords and perform automated attacks.

Before we get into the meat of this chapter let's take a look at some actual Linux password hashes. Below are two Linux password hashes, the first is from Metasploitable2, the second is a user I made on my Kali Linux box.

+   1. msfadmin:$1$XN10Zj2c$Rt/zzCW3mLtUWA.ihZjA5/
+   2. dan:$6$miC/IqYE$eAHWWJ2S61YKukO.Amlriu4JNCru9vkcyzFndynlrJGF6QjfCjV0Sd70CSmX0Sp9xmthpr11yOR4QTSpJCYN/

The big difference between NTLM passwords and Linux passwords, is that Linux passwords are salted. The salt is a unique string that is used to encode each password making the password hashes different even if two users used the exact same password. This way no two hashes are ever the same.

We break down the contents of the password hash below: