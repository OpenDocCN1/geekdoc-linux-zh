indicated, an entry applies to users who don't fall into a class that already has file-limit defined.

# Data limits

Instead of limiting the number of files a user can transfer, you can limit the amount of data that can be transferred by a user. Here are some examples:

```
byte-limit    total    102400000    home
byte-limit    out      51200000    world
byte-limit    in       25600000    world
```

The byte-limit parameter limits the amount of data transferred during a session to a certain number of bytes. The first line shows that the total amount of data that a user in the home class can transfer during a session (both in and out) is 102400000 bytes (about 100MB). Someone assigned to the world class can take (out) only 51200000 bytes of data during an FTP session (about 50MB). A user in the world class can also upload only 25600000 bytes of data during a session (about 25MB).

> **NOTE:** If a user reaches the end of the byte-limit value during a transfer, the transfer is allowed to complete before the connection is dropped.

# Connection time limits

You can limit the amount of time that an anonymous or guest user can be connected during an FTP session with the limit-time parameter. There is no way to limit connection time for any real users. By default, anonymous and guest users aren't limited either. For example:

```
limit-time anonymous 120
limit-time guest      240
```

In this example, the anonymous user is limited to sessions that are 120 minutes long. A guest user, however, is limited to 240-minute sessions.

# Denying access from hosts and users

You can deny certain host computers from having access to your FTP server. Likewise, you can deny access for anonymous, guest, and real accounts in different ways.

# Denying access to host computers

You can deny FTP access to requests coming from specific hosts using the deny parameter. Here's an example:

```
deny    maple,snowbird,oak    /etc/ftpdeny.msg
```

In this example, any user who tries to log in to your FTP service from computers named maple, snowbird, or oak will be denied access to your system. After the user tries to log in, a message from a specified text file (in this example, /etc/ftpdeny.msg) is displayed to