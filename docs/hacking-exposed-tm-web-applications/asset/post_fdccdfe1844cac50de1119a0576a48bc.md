
# 134 Hacking Exposed Web Applications

Wait a second—where is the username and password? Per the Basic authentication spec, the authentication credentials are sent in the Authorization header in the response, but they are encoded using the Base 64 algorithm, making them appear to have been encrypted or hashed, leading people to a false sense of security. In reality, Base 64 encoding is trivially reversible using any popular Base 64 decoder. Here is a sample Perl script that does the job of decoding Base 64 strings:

```
#!/usr/bin/perl
# bd64.pl
# decode from base 64
use MIME::Base64;
print decode_base64($ARGV[0]);
```

Let's run this bd64.pl decoder on the value we saw in our previous example of Basic authentication in action:

```
C:\bd64.pl dGVdp0ZXXNO
test:
```

As you see, Basic authentication is wide open to eavesdropping attacks, despite the inscrutable nature of the value it sends in the Authorization header. This is the most severe limitation of the protocol.

There are a couple of things to think about Basic authentication. One is that most browsers, using Internet Explorer and Netscape, will cache Basic credentials and send them automatically to all pages in the realm, whether its SSL or not. This means you can't have an HTTPS login page and other pages that are HTTP-based without compromising the confidentiality of the password. The only way to change the password is to request the user to close the browser or force the browser to close at the page.

Another issue with Basic auth is how it is implemented in Microsoft's IIS. Basic auth requires Windows account credentials to work on IIS, and authenticated users will be treated as interactive logins (or in other words, accounts must have “Log on locally” permissions to use Basic auth).

Finally, by its simple nature, Basic authentication is easily passed through proxy servers. This compares favorably to other authentication schemes like Integrated Windows (discussed in an upcoming section), which cannot pass proxy servers that implement the Windows authentication protocol (these are rare to nonexistent on the Internet).

In summary, Basic authentication provides a very simple authentication mechanism with a standard user interface that can function across proxy servers. However, since the authentication credentials are effectively sent in the clear, this authentication method is subject to eavesdropping and replay attacks. The use of 128-bit SSL encryption can thwart these attacks, and is strongly recommended for all Web sites that use Basic authentication.

# Chapter 5: Authentication

## Digest

Digest authentication was designed to provide a higher level of security than Basic authentication. It is described in RFC 2617. Digest auth is based on a challenge-response authentication model. This is a common technique used to prevent that someone not send the secret in cleartext that would be subject to eavesdropping.

Digest authentication works similarly to Basic authentication. The users and the server reply with WWW-Authentication header indicating credentials required to access the requested resource. But instead of sending the username and password in Base64 encoding as Basic, the server challenges the client with a random value called a nonce. The browser then uses a one-way cryptographic function to create a message digest of the username, the password, given the nonce, the HTTP method, and the requested URI. A message digest function, also known as a hashing algorithm, is a cryptographic function that is easily computed in one direction, and computationally infeasible to reverse. Compare with Basic authentication, where reversing. Any hashing algorithm can be specified within the server channel; RFC 2617 describes the use of the MD5 hash as the default.

Why not just use the user's password directly? Although they differ in other cryptographic protocols, the use of a nonce in Digest authentication is similar to the use of salts in other password schemes. It is used to create a larger key space to make it more difficult for someone to perform a database attack against compromised passwords. Consider a large database that store the MD5 hash of all words in the dictionary and all permutations of characters with less than alphanumeric characters. The attacker would just have to compute the MD5 hash of each one, and subsequently make one query to the database to find the password associated with the MD5 hash. The use of the nonce effectively increases the key space and makes the database attack infeasible by requiring a database that is much larger.

Digest authentication is a significant improvement over Basic authentication, primarily because its cleartext password is not passed over the wire. This makes it much resistant to eavesdropping than Basic authentication. Digest authentication is still vulnerable to replay attacks, since the digest in the response will grant access to the requested resource even in the absence of the user's actual password. However, because the original resource is included in the message digest, a replay attack should only permit access to the specific resource (assuming Digest auth has been implemented properly). To protect against replay attacks, the nonce could be built from information that is difficult to spoof, such as the digest of the client IP address and a timestamp.

> Microsoft's implementation of Digest auth requires that the server have access to the cleartext of the user's password so that digests can be calculated. Thus, implementing Digest authentication on Windows requires that user passwords be stored using reversible encryption, rather than using the standard one-way MD4 algorithm.

# Hacking Exposed Web Applications

For those who like to tinker, here's a short Perl script that uses the Digest::MD5 Perl module from Neil Winston to generate MD5 hashes:

```
#!/usr/bin/perl
# md5-encode.pl
# encode using MD5
use Digest::MD5 qw(md5_hex);
print md5_hex($ARGV[0]);
```

This script outputs the MD5 hash in hexadecimal format, but you could output binary or Base 64 by substituting qw(md5) or qw(md5_base64) at the appropriate spot in line 4. This script could provide a rudimentary tool for comparing Authentication strings to known values (such as cracking), but unless the username, Nonce, HTTP method, and the requested URI are known, this is a fruitless endeavour.

An interesting tool for cracking MD5 hashes MDCrack is available from Gregory Duchemin (“References and Further Reading” at the end of this chapter for a link).

## Integrated Windows (NTLM)

Integrated Windows (formerly as NTLM authentication and Windows challenge/response authentication) uses Microsoft’s proprietary NT LAN Manager (NTLM) authentication algorithm over HTTP. Because it uses NTLM rather than a standard digest algorithm, it only works Microsoft’s Internet Explorer browser and IIS servers. Because most sites want to support multiple browsers, they do not implement Integrated Windows authentication. This makes Integrated Windows auth more suitable for intranet deployment.

Integrated Windows works much in the same way as Digest authentication, using a challenge-response mechanism. When a client requests a resource protected by Integrated Windows, the server responds with an HTTP 401 Access Denied and a WWW-Authenticate: NTLM [challenge] header. The [challenge] value contains a digest of the NTLM nonce and other information to the request. Internet Explorer will then find the NTLM credentials for the currently logged-on user, use the NTLM algorithm to hash the challenge value, and provide the hashed value in an HTTP response with Authorization: NTLM [response] header. If these credentials fail three times, Internet Explorer prompts the user with the dialog shown in Figure-5.

The user may now enter the correct username, password, and domain, and the process repeats itself. The key thing to realize about Integrated Windows authentication is that no version of the user’s password ever crosses the wire. This provides fairly robust security against eavesdropping attacks.

> Older versions of the NTLM algorithm are vulnerable to eavesdropping attacks (specifically, the LM algorithm). Although these versions are not used in HTTP-based authentication, it’s a good idea to specify Windows systems use the newer versions, according to Microsoft Knowledge Base Article Q147706.
