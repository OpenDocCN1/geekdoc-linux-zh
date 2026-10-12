posts made by your readers back to your Diablo system, and it will feed those posts to the rest of Usenet through your peer feeds. Diablo is not quite as automated as INN. Although INN may be more complex to install and configure, I believe it is your best bet in the long run for supporting readers.

# Using nntpcache

If you want to outsource most of your news, yet you would still like to have some local newsgroups, nntpcache is something you should look into.

Installing nntpcache is fairly simple. Just untar, configure, and make. The INSTALL file that comes with the source distribution has a cookbook configuration that is the default. If you are outsourcing your news to a third-party provider, you will want to tweak this a bit.

The nntpcache.servers file in Listing 23.2 is where most of your configuration will take place.

# LISTING 23.2 The nntpcache.servers File

```
/*
# This file defines which nntp servers nntpcache uses. The reason for the
# Interface address is that if you're connecting to more than one server it
# probably means you have more than one gateway, which may well mean you
# have more than one IP address, so nntpcache allows you to configure
# which one of them you connect to each server as. A bind address of
# 0.0.0.0 or DEFAULT will select the system default address.

# A timeout of 0 means not to cache anything of that type from the
# specified server. Use this for servers on the same machine or on a
# fast local ethernet or when using nntpcache as a mere proxy.

# As in nntpcache.access, this file is parsed from the general to the
# specific, from the top to the bottom. The LAST MATCH IS DOMINANT
#
#                  /*          timeouts          */
# host:port    Interface    Active  Act.tim Newsg rp Group Xover Arts

# the localhost:120 entry below is for an INN news-server running on
# localhost, port 120. We use this to serve local groups
localhost:120  localhost    30m     24h     24h     10m     0m      0m

# Change this to the name of your main NNTP news feed. We run a
```