19. What will be the effect of a computer having the following two lines in `/etc/ntp.conf`?
server pool.ntp.org
server tardis.example.org

+   A. The local computer's NTP server will poll a server in the public NTP server pool; the first `server` option overrides subsequent `server` options.

+   B. The local computer's NTP server will poll the `tardis.example.org` time server; the last `server` option overrides earlier server options.

+   C. The local computer's NTP server will poll both a server in the public NTP server pool and `tardis.example.org` and use whichever site provides the cleanest time data.

+   D. The local computer's NTP server will refuse to run because of a malformed `server` specification in `/etc/ntp.conf`.

20. You've configured one computer on your five-computer network, `gateway.pangaea.edu`, as an NTP server that obtains its time signal from `ntp.example.com`. This configuration provides an acceptably accurate clock on `gateway.pangaea.edu`. What computer(s) should your network's other computers use as their time source(s)?

+   A. You should consult a public NTP server list to locate the best server for you.

+   B. Both `gateway.pangaea.edu` and `ntp.example.com`.

+   C. Only `ntp.example.com`.

+   D. Only `gateway.pangaea.edu`.