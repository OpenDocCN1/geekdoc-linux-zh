```
ec_negl( r = inet_pton(AF_INET, "66.218.71.94", &ipv4) )

if (r == 0)
    printf("Can't convert\n");
else {
    ec_null( inet_ntop(AF_INET, &ipv4, ipv4str, sizeof(ipv4str)) )
    printf("%s\n", ipv4str);
}

ec_negl( r = inet_pton(AF_INET6,
    "FEDC:BA98:7654:3210:FEDC:BA98:7654:3210", &ipv6) )

if (r == 0)
    printf("Can't convert\n");
else {
    ec_null( inet_ntop(AF_INET6, &ipv6, ipv6str, sizeof(ipv6str)) )
    printf("%s\n", ipv6str);
}

return;

EC_CLEANUP_BGN
    EC_FLUSH("cvt")
EC_CLEANUP_END
)
```

The output from calling this function:

66.218.71.94
fedc:ba98:7654:3210:fedc:ba98:7654:3210

# 8.10 High-Performance Considerations

I showed an example of a Web server in Section 8.4.4, using the multiple-client approach from Section 8.1.3. Imagine now that our Web server is trying to handle 1000 clients at once. Or 10,000. Will it work?

Let's make a list of what the so-called “C10K” ("clients 10,000") problems might be with our simple example:

+   - select has to look at up to 10,001 file descriptors. That's probably bigger
+     than an fd_set can hold. Even if it can hold that number, it would take
+     select a long time to process them all.
+   - There's a limit on how many file descriptors a process can have open, and
+     it's usually much less than 10,001.
+   - To provide decent response, we'd want to engage multiple processes or mul-
+     tiple threads to handle all the work, but there's a limit on those resources, too.