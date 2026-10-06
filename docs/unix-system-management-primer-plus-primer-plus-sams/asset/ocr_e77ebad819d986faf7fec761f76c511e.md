acceptable, you can proceed with the installation. A typical Perl regression test on Solaris 8 looks like this:

```
base/cond..................................ok
base/if.....................................ok
base/lex...................................ok
base/pat...................................ok
base/rs....................................ok
base/term..................................ok
comp/bproto...............................ok
comp/cmdopt...............................ok
Some output skipped.
lib/textwrap..............................
lib/thr500....... skipping test on this platform
lib/tie-push..............................ok
lib/tie-refresh............................ok
lib/tie-splice............................ok
lib/tie-stdarray.........................
lib/tie-stdhandle........................
lib/tie-stdpush..........................
lib/tie-substrhash.......................
lib/timelocal.............................
lib/trig..................................ok
All tests successful.
u=0.53 s=0.81 cu=41.2 cs=18.72 scripts=265 tests=13145
```

In this example, all 13,145 tests were successful, and any operations implemented in this particular build were skipped.

# # Alpha and Beta Testing

Every test described up to this point is performed by internal staff, including the QA department, the people who develop the applications, and the administrators who maintain the systems applications run. However, none of this internal testing assesses how the system or application will perform or be perceived in the real world. When your internal testing is complete (unit tests, load tests, regression tests, and any other tests you decide to perform), it's time to test the system with real users; these are the alpha and beta tests.

# # Recruiting Users for Your Tests

User recruitment is the most critical part of alpha and beta testing. To recruit users, tell them of the test and offer an incentive for their participation. Typically, technically oriented and computer savvy users are the most likely to jump at the opportunity to test a new product. This type of user, however, might not represent the majority of your product's ends, especially in the world of ISPs.

You can use a variety of methods to announce your tests, but the most effective announcements will be in places that are viewed daily by your user base. Some appropriate places to consider include the following: