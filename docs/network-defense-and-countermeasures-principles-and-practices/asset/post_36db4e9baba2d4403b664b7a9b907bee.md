
# 138 CHAPTER 5 Intrusion-Detection Systems

## EXERCISE 5.3: Open Source Honeypots

Note: This exercise requires you to use an open source honeypot. One such free solution can be found at www.honeypotproject.org, but feel free to use any honeypot you like. In fact, if possible, it is best to test out multiple solutions in order to compare results.

- 1. Install the honeypot on a lab machine.
- 2. Configure it according to the vendor documentation.
- 3. Have one student(s) as a hacker attacking the honeypot.
- 4. The other student(s) should use the honeypot to detect intrusion.

## EXERCISE 5.4: Recommend an IDS

- 1. Assume you are working for a small organization that has a moderate security budget.
- 2. Select a particular IDS solution you would recommend for organization.
- 3. Write your recommendations, including your reasons, in a memo format as if submitting them to a CIO or other decision maker.

# PROJECTS

## PROJECT 5.1: IDS Strategy

Using websites and vendor documentation, create a document that outlines a complete IDS plan for a network. Plan your entire IDS strategy assuming a budget of $2,000.

## PROJECT 5.2: Firewall-Based IDS

Using web resources, books, or other resources as well as your own opinions, determine whether you think a firewall-based IDS or a separate IDS is a better solution. Write a memo (as if you were submitting it to a CIO or other decision maker) explaining your position, including reasons for coming to this conclusion.

## PROJECT 5.3: How to Improve Honeypots

By now you should have a good understanding of how honeypots work, and you should have actually used at least one honeypot. But all security technology, honeypots, are evolving. Describe, in detail, at least two improvements you would like to see in honeypot technology. This could include features not currently available, improved detection, or more aggressive responses. The following sites describe current honeypot technology and might be of use to you.

- www.projecthoneypot.org/
- https://www.sans.edu/cyber-research/security-laboratory/article/honeypots-guide
- https://www.computerworld.com/article/2573345/security0/honeypots--the-sweet-spot-in-network-security.html

# Chapter 6

# Encryption Fundamentals

## Chapter Objectives

After reading this chapter and completing the exercises, you will be able to do the following:

- Explain encryption concepts.
- Describe the history of encryption and modern encryption methods.
- Use some simple decryption techniques.

# Introduction

Encryption is a vital part of any network security strategy. No matter how secure the network is, if the data is not encrypted at rest or during transmission, then that data is vulnerable. Even most basic wireless routers for home users now offer encryption.

This chapter offers a basic overview of encryption and an explanation of how it works to help you make good decisions for your organization. A complete examination is the reward of this book, but this chapter provides a “manager’s understanding” of cryptography to help you ask the right questions about your organization’s encryption needs.

# The History of Encryption

Encrypting communications is a very old idea. People have found the need to send private communications for most of the history of civilization. The need for privacy originally arose from military and political needs, has expanded beyond that. Businesses need to keep data private to maintain a competitive edge. People want to keep certain information, such as their medical records and financial records, private.

For much of human history, private communications meant encrypting written communiqués. Over the past century that has expanded to radio transmission, telephone communications, and computer/Internet communications. In the past several decades, the encryption of computerized communications has actually become commonplace. In fact, you can find computer/Internet communications encrypted more than phone or radio. The digital environment makes implementing a particular type of encryption much easier.

Whatever the nature of the data you are encrypting, or the nature of transmitting the data, the basic concept is actually quite simple. Messages must be changed in such a way that they cannot be read easily by any party that intercepts them but can be decoded easily by the intended recipient. In this section, you will examine a few historical methods of encryption. Note that these are very old methods, and cannot be used for secure communication today. An amateur could easily crack the methods discussed in this section. However, they are wonderful examples for conveying the concept without incorporating a great deal of math, which is required of the more complex encryption methods.

> FYI: False Claims About Encryption
>
> As you will see in this chapter, the basic concepts of encryption are very simple. Anyone with even rudimentary programming skills can write a program that implements one of the simple encryption methods examined here. However, these methods are not secure and are included only to illustrate fundamental encryption concepts.

# The Caesar Cipher

One of the oldest recorded encryption methods is the Caesar Cipher. This name is based on the fact that each character in the encrypted text is shifted a fixed number of places down the alphabet. This method is simple to implement, requiring no technological assistance. You choose some number by which to shift each letter of the text. For example, if the text is "cat" and you choose to shift by two letters, then the message becomes "ecv". Or, if you choose to shift by three letters, it becomes "fdw".

In this example, you can choose any shifting pattern you like. You can shift to the right or left by any number of spaces. Because this is a simple method to understand, it makes a good place to start your study of encryption. It is, however, extremely easy to crack. You see, any language has a certain letter and word frequency, meaning that some letters are used more frequently than others. In the English language, the most common single-letter word is "a". The most common three-letter word is "the". These two characteristics could help you decrypt a Caesar cipher. For example, if you saw a string of nonsense letters and noticed a three-letter word in the message, you might easily sure this word was "the"—and the odds are high in favor of this being correct.

Furthermore, if you frequently noticed a single-letter word in the text, it is most likely the letter "a". You now have found the substitution scheme for a, t, and e. You can now translate all of these letters in the message and attempt to or simply analyze the substitute letters for a, t, and e and derive the substitution cipher that was used for this message. Decrypting a message of this type does not even require a computer. Someone with no background in cryptography could do it in less than ten minutes using pen and paper.

Caesar ciphers belong to a class of encryption algorithms known as substitution ciphers. The name derives from the fact that each character in the encrypted text is shifted a fixed number of places down the alphabet. The particular substitution scheme used (for example, 12 or 11) in a Caesar cipher is called a substitution alphabet (that is, b substitutes for a, u substitutes for t, etc.). Because one always substitutes for one other letter, the Caesar cipher is sometimes called a mono-alphabet substitution method.

The Caesar cipher, like all historical ciphers, is simply too weak for modern use. It is presented here just to help you understand the concepts of cryptography.

# ROT 13

ROT 13 is another single alphabet substitution cipher. All characters are rotated 13 characters through the alphabet.

The phrase

A CAT

becomes

N PNG

ROT 13 is a single-substitution cipher.
