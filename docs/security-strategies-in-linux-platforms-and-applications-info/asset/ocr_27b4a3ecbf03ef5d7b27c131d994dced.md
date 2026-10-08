# PART 3 | Building a Layered Linux Strategy

However, mailing lists are generally not suited for very long log files. Some users may look about the inclusion of all the most relevant excerpts of a log file as little better than span.

Be aware, Linux mailing lists may still be a venue for flame wars. It is in some ways a tradition that goes back to the first debates between Linus Torvalds and Andrew Tannebaum, the founder of Minix, on the nature of an appropriate kernel for any operating system. Not all us can manage a flame war as well as Torvalds and Tannebaum, so do not be afraid to walk away. Sometimes, it is the best way to preserve the goodwill of the Linux community.

Red Hat and Ubuntu sponsor mailing lists on a substantial number of topics. For more information, see https://www.redhat.com/mailman/listinfo/ and https://lists.ubuntu.com/. They also sponsor a wide variety of message boards. The basic principles that apply to sharing information on mailing lists also apply to message boards.

# New Components Before Putting Them into Production

Open source software is excellent. For example, the Apache Web server would not have become dominant on the Internet unless it provided top-notch secure features. Open source developers do their best to test their software with every major combination of hardware and software, within reason. But they can't test every possible combination. In rare cases, mistakes do happen.

So you should test every update before putting it into production. It can help others if you document the results. One way to jump ahead in the test cycle is to participate in the beta phase of software, before new features are officially released

One axiom of testing is that you should always keep a version of the existing software configuration. If the testing fails or if a problem arises after you put the new or updated component into production, you will be able to restore the older working configuration.

# Test Updates

Especially in mission-critical applications and services, it's important to test new open source software before putting it into production. The same proviso applies if you're installing a new version of a software package.

With preproduction testing, it's important to make sure the service or application works as intended. It's important to test the system under simulated production conditions to confirm that the updated software can still handle the demands of your users.

If you've used the application or service before, you may have custom settings or configuration files from the previous version of the software. While developers normally strive to retain backward compatibility; that does not always happen. So if you have custom configuration files for older versions of recently updated software, if the new version of the software functions at least as well with the older configuration file, you can install upgrade on a production system with confidence. You can then incorporate the new features associated with the upgrade at your convenience.