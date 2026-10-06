On a larger scale, if you reconfigure a server to authenticate your user accounts against your Windows 2000 domain controller instead of the Unix /etc/passwd file, you would want to verify that every application that depends on the system's authentication subsystem successfully authenticate using Windows usernames and passwords. You may find that although Windows allows usernames of up to 20 characters, certain Unix applications do not accept usernames longer than 8 characters. This is a serious compatibility issue that could cause you to back out of your new authentication mechanism completely.

As you can see, the tests for these two examples were vastly different due to the nature of their dependent components. Generally, you will want to perform unit tests (as described in earlier sections of the chapter) to test all of the functionalities between the changed component and its dependencies.

# A Compatibility Test Example

The IT department at a small company was using Request Tracker (RT) version 1 for trouble ticket management (see Chapter 5, "Support Administration," for more information on RT). RT v1's limitations forced the company to consider an upgrade to RT version 2. The system administrator wasted time and upgraded to version 2 without reading any of the known bugs listed in its documentation.

Right away, users experienced problems—pages would periodically come up blank and searches on existing tickets produced no results. Eventually, the system administrator read the product documentation and saw that RT 2 was not compatible with Perl 5.6.0, the version installed on that system.

Not wanting to revert to RT version 1, he compiled and installed Perl 5.6.1, which was documented to work with RT 2. Instead of replacing the current version of Perl, he installed it in a nonstandard location so it would not interfere with other programs using Perl—the last thing he wanted

The administrator reconfigured RT to use the new version of Perl and redeployed it. It functioned normally, without any blank pages or empty searches.

This example demonstrates the results of a simple software incompatibility, how it was remedied, and how a simple task like reading product documentation could have prevented this situation from happening at all. Note how the system administrator left the current version of Perl alone so as not to disturb the system further—considering the number of Perl scripts on the system, this could have introduced even more compatibility issues.

# Read the Product Documentation

Always read the documentation, especially the sections on requirements and known bugs, for any product you want to install on your systems.