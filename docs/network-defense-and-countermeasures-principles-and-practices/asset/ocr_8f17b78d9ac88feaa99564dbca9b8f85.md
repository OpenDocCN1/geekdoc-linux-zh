# The History of Encryption

For much of human private communications meant encrypting written communiqués. Over the past century that has expanded to radio transmission, telephone communications, and computer/Internet communications. In the past several decades the encryption of computerized communications has actually become commonplace. In fact you can find computer/Internet communications encrypted more than phone or radio. The digital environment makes implementing a particular type of encryption much easier.

Whatever the nature of the data you are encrypting, or the nature of transmitting the data, the basic concept is actually quite simple. Messages must be changed in such a way that they cannot be read easily by any party that intercepts them but can be decoded easily by the intended recipient. In this section you will examine a few historical methods of encryption. Note that these are very old methods, and cannot be used for secure communication today. An amateur could easily crack the methods discussed in this section. However, they are wonderful examples for conveying concept without incorporating a great deal of math, which is required of the more complex encryption methods.

> FYI: False Claims About Encryption

As you will see in this chapter, the basic concepts of encryption are very simple. Anyone with even rudimentary programming skills can write a program that implements one of the simple encryption methods examined here. However, these methods are not secure and are included only to illustrate fundamental encryption concepts.

From time to time new to encryption discovers these basic methods, and in enthusiasm attempts to create his own encryption method by making some minor modifications. Although this is a stimulating intellectual exercise, it is only that. Users without training in advanced math or cryptography are extremely unlikely to stumble across a new encryption method that is effective for secure communications.

Amateurs frequently post claims that they have discovered the last, unbreakable algorithm on the Usenet newsgroup.scrypt (if you are not familiar with Usenet, those groups are not accessible via the Groups link on www.google.com). Their algorithms are usually quickly broken. Unfortunately, some people implement such a method into a software product and market it as secure.

Some distributors of insecure encryption methods and software are so out of simple greed and are intentionally defrauding an unsuspecting public. Others do so out of simple ignorance, honestly believing that their is superior. Methods for evaluating encryption claims are discussed later in this chapter.

# The Caesar Cipher

One of the oldest recorded encryption methods is the Caesar Cipher. This name is based on a claim that this method was used by ancient Roman emperors. This method is simple to implement, requiring no technological assistance. You choose some number by which shift each letter of a text. For example, if the text

A cat