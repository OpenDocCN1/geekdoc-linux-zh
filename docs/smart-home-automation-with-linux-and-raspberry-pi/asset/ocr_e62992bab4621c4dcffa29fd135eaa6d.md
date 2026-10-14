Sending multiple messages to a group of users is possible through most, if not all, SMS gateway APIs, but their administration is usually through the Web. And because you have a fully empowered Linux box controlling your environment, you might as well store the addresses on your machine and send multiple messages that way. The cost is the same, and the time difference is generally negligible. I’ll expand the SMS script in Chapter 7.

# Receiving Messages

This is no more difficult than sending messages, but it does require some extra steps—and, if you’d like your own custom number, more cost. In either case, the SMS gateway company receives a message on your behalf and then passes it onto you via an alternate, commonly agreed protocol so that you can do something specific with it. Depending on the company, service level, and API, you might be able to do the following:

+   - Forward the text message as an e-mail
+   - Request a web page with the sender and message as arguments
+   - Send an autoresponse
+   - Forward to another (mobile) number

The two of interest here are the e-mail and web page handlers. In either case, the text-based format of SMS means that parsers are generally trivial to write.

Sending the message from a phone can happen in a couple of ways. The cheapest way is to share a number with other users. In this case, you will send a message, which includes your username, to the number supplied by your SMS gateway. The gateway then looks up the given user with a target machine and issues a request. The format of this message might be as follows:

```
username-your message here
```

or as follows:

```
username your message here
```

or even as follows:

```
null your message here
```

In the latter case (as adopted by Txtlocal), the gateway looks up the phone number from which you’re sending the request and ties it to your account information, before passing the message on. It is also up to the gateway whether this username (or null) is included in the message.

> **Tip** Choose a short username if possible to save SMS characters! You can save repeatedly writing your username if you save a version in your drafts folder and copy it out each time.

Alternatively, you can purchase a specific number for our own use. In that case, you don’t have to include the username in the message anymore. This route usually incurs a setup fee. For those with even more money, you can buy a special short code (between four and six digits) that is an alias to the longer form of the number. These are usually used for businesses, however, and are priced accordingly. They might be easier to remember, but you only really need them when your phone has died, making your address book inaccessible. In which case, carrying a written copy of the number is cheaper!