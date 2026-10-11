4. The **options** statement in this case should tell the forwarding name server where to forward its requests. This is done in this format:

```
```
options {
    forwarders 192.168.90.9;
};
```
```

5. A client machine should maintain its own cache unless it does not have the spare hard drive space to so do. Add the caching statement with the following:

```
```
zone "." {
    type hint;
    file "My.cache";
};
```
```

6. For all other zones, you use the forwarding statement format. So, the next three statements might look like this:

```
```
zone "0.0.127.in-addr.arpa" {
    type forward only;
};
zone "animals.org" {
    type forward only;
};
zone "90.168.192.in-addr.arpa" {
    type forward only;
};
```
```

7. Determine what other types of statements you might want to include. Some people will try to attack a machine through the name service port, so it is a good idea to do some form of logging:

```
```
logging {
    channel {
        file "/var/log/named.log";
        severity warning;
    };
    category lame-servers {
        null;
    };
};
```
```