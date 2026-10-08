
# Hacking Exposed Web Applications

exposition (there are probably a few sites with desires of world domination, as well). Client-side techniques rely on sending the "state information" to the client and trusting the client to return this information unchanged. In short, the client cannot be trusted. Any time information leaves the server, a cookie value, for example, the client can modify cookie to contain arbitrary information. If you run into a Web server that performs state management, it is a safe bet that state information is being passed to the client. It is also likely to be insecure.

Client-side techniques are used regularly, they must have some advantages. The primary advantage of client-side techniques is that they work particularly well in a load-balanced architecture with a Web farm. Incoming requests can be distributed to the least busy server without worrying how the server is supposed to respond. The server inspects the state information, looks up in the database, checks the shopping cart, and returns the appropriate data. On the other hand, load balancers are becoming increasingly intelligent and can handle single sessions that touch multiple servers. Now, let's take a look at some of the carriers for state information.

## Hidden Fields

Hidden forms are easy to identify, so we'll start with this category. A hidden field does not imply poor security, but it can be an indicator. Let's take a look at what a FORM created from an application's login page

```html
<FORM name=login_form https://login.victim.com/config/login4r0naidr6d3 method=post>
<INPUT name=Tries type=hidden><INPUT value=us name=I8N type=hidden>
<INPUT name=Bypass type=hidden><INPUT value=64mbvjoubdp06 name=hidden type=hidden><INPUT value=pVj3sXMRJKD8lggZTYDLWNY_name=Challenge type=hidden>
User Name:<INPUT name=Login>
Password:<INPUT type=password maxLength=32 value="" name=Passwd>
```

When the user submits their username and password, she is actually submitting seven pieces of information to the server even though only two were visible on the Web page. Table 7-2 summarizes these values.

From this, it appears that two hidden fields are tracking state information, "Tries" and "U". At this point it is not clear whether a vulnerability exists. Remember, we need to identify all of the state mechanisms first.

> As we continue to look at session management techniques, we are sure to touch on other aspects of Web security. Session management is crucial to the manner in which applications handle authentication and authorization. Plus, data collected from the client are always subject to input validation and attacks. Security testing really requires a holistic view of the application.

## Chapter 7: Attacking Session State Management

| Value | Description |
| --- | --- |
| Tries | Probably represents the number of times the user has tried to log to the account now since we haven't submitted a password yet. If we wanted to launch a brute-force attack, we would try to keep this number at zero. The server might lock the account if this value passes a certain threshold. Potential Vulnerability: The application enforces account lockouts to protect itself from brute-force attacks; however; the lockout variable is carried on the client side and can be trivially modified. |
| I8N | The value for this field is set to "us". Since it appears to handle the language for the site, changing this value might not have any security implications for a session. Potential Vulnerability: The field could still be vulnerable to input validation attacks. Check out Chapter 8 for more information. |
| Bypass | Here's a field name that sounds exciting. Does bypass require a specific string? Or could it be a Boolean value that lets a user log in without requiring a password? Potential Vulnerability: Bypass the login page as an authorization attack (Chapter 6). |
| U | The unknown field. This could contain a session identifier or application information. At the very least, it merits investigation. Check out the "SessionID Analysis" section later in this chapter for ideas on how to examine unknown values. Potential Vulnerability: May contain sensitive information that has been encoded (easy to break) or encrypted (difficult to break). |
| Challenge | This string could be part of a challenge-response authentication mechanism. |
| Login | The user's login name. |
| Passwd | The user's password. |

Table 7-2. Hidden Field Example Values

## The URL

Take another look at the FORM example from the previous section. There was another hidden "field" in the action element of the FORM:

```html
<FORM name=login_form action=https://login.victim.com/config/login?4fr0naidr6d method=post>
```

Session variables do not have to be in SETs for the order to track the them. The server can set parameters or redirects customized to a specific user. Other examples might look like this:

```
/redirect.html/103-673347-6580661/
/ViewBase#sidrS5J5iOEEACi6r0E2ksQJnUEiakKFH/
/index.php?session_id=E3DF0FC4C-E5F7-4844-8DD9-4808906D85
```

In the latter case, the "sid" name gives the session ID. Carrying the session ID in the URL is not insecure, but there are many points to keep in mind.

- *HTTPS*: If the session ID can be decoded from another computer, a malicious user could cleartext HTTP connections in order to spoof other users.
- *Bookmarks*: A user might bookmark a URL that includes a session ID. If the application session IDs or removes them (if it has a small pool), then the bookmark will be invalid when the user returns.
- *Content*: This applies to any client-side session ID. If the content can be decoded, then the session ID is insecure. Check out the "SessionID Analysis" section in this chapter for more.

## HTTP Headers and Cookies

Cookie values may be the most common method. Ephemeral (non-persistent) cookies are used to track state. The browser will delete them when it closes. Persistent cookies are stored on the user's computer. Here's an example:

```
Set-Cookie: NAME=VALUE; expires=Sat, 01-Jan-2023 00:00:00 GMT; path=/; domain=DOMAIN_NAME
```

This means the cookie is sent over HTTP. Sites that "Remember me" use persistent cookies. Here's an example:

```
Set-Cookie: autolog=bWlrZteXMzYIdA3D%3D%3D; expires=Sat, 01-Jan-2023 00:00:00 GMT; path=/; domain=victim.com
```

## Expire Times

When you log out of an application that uses persistent cookies, the usual behavior is to set the cookie value to NULL with an expire time in the past. This erases the cookie. An application might also use the expire time to force users to reauthenticate every 20 minutes. The cookie would only have a valid period of 20 minutes from the user first authenticated. When the cookie has expired, the browser deletes it. The application disappears and asks the user for new credentials. This sounds like an effective method of timing out sessions, but only if it is done correctly. If the application sets a "password" that expires in 20 minutes:

```
Set-Cookie: HasPwd=451jh28f;expires=Tue, 17-Apr-2002 12:00 GMT; path=/; domain=victim.com
```

then extend the expire time and see if the server honors the cookie:

```
Set-Cookie: HasPwd=451jh28f;expires=Tue, 17-Apr-2003 12:00 GMT; path=/; domain=victim.com
```

This is how you can determine if there are any server-side controls on session times. If this new cookie, valid for 20 minutes plus one year, lasts for an hour, then you know that the 20-minute window is arbitrary—the server is enforcing a hard timeout of 60 minutes.

## HTTP Referer

We've seen sites use the HTTP Referer (yes, that's spelling) header for session and authentication handling. This is similar to passing the state in the URL, but the data have to be captured with a tool like Achilles.

## SERVER-SIDE TECHNIQUES

Server-side session tracking techniques tend to be stronger than those that transmit information to the client. Of course, no server-side technique keeps all of the state information from the client. After all, it is necessary to identify the user. The difference with a server-side technique is that state information such as profile, privileges, and shopping cart information are all stored on the server. The client only passes a single session ID as identification.
