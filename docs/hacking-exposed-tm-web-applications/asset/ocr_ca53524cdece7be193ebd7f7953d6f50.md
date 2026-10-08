# Chapter 7: Attacking Session State Management

The fourteen bytes remain constant. This means the encrypted data come from a static source, the username, or first name, or a flag for “e-mail me a reminder.” It could also imply that it's an entirely encrypted string and merely concatenated to the previous eight bytes. As you can see, we're starting to get pretty vague.

The final two bytes are unknown. The data is short, so we could guess that it's only a counter or some similar value that changes, but does not represent a lot of information, and it could be a checksum for the previous data, added to ensure no tampered with the cookie.

There is a class of attacks that can be performed on an encrypted cookie. They can be referred to as “diddling” because you change portions of the encrypted string and monitor changes in the application's performance. Let's take a look at an example cookie and three modifications:

```
Original:
Modification 1: 4zDAREYhcvcfqpSY3FOTGMbm3
Modification 2: 4zDAREYhcAAAAAAAAAAAAAAAm3
Modification 3: 4zDAREYhcvcfqpSY3FOTGMbm3
Modification 3: 4zDAREYhcvcfqpSYYvffqpSym3
```

We're focusing on the static, 14-byte field. First, we try all similar characters. If the cookie is accepted on a login page, for example, then the server does not inspect the portion of data for authentication credentials. If the cookie is rejected on the page for viewing the user's profile, then we find that portion contains some user information.

In the second case we change one letter. Then, we'll have to submit the cookie to different portions of the application to see where it is accepted and where it is rejected. Maybe it represents a flag for users and superusers? You know never. (But you'd be extremely lucky!)

In the third case we repeated the first half of the hash. Maybe the format is username:password. If we make this change, causing the login page rejects it, we're on the right track. This can quickly become long, unending guesswork.

As an application programmer, the methods that make a more secure MD5 hash make a more secure encrypted string. Place the most dynamic data at the beginning of the string. In CBC (a method in which each subsequent block is encrypted based on the encrypted output of the previous block), this removes many of the trends visible with static data. Additionally, place a checksum at the end of the string. The checksum should be easily generated and identify any modifications to the string contents. This protects you from “diddling” attacks such as the one described above.

```
checksum = foo( salt + time + static data )
String = 3DES( salt + time + static data )
```

For tools to help with encryption and decryption, try the Unix crypt() function, Perl's Crypt::DES module, and the mycrypt library (http://my.hellug.org/).