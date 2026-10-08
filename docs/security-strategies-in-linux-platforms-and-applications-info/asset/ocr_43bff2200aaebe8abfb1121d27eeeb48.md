# Basic Asterisk Configuration

Asterisk configuration files are typically installed in the /etc/asterisk/ directory. Most of the configuration filenames relate to different features. Asterisk configuration is centered around the dialplan, which can be a directory, a set of menu options, or even a group of channels. These are known as contexts, and can be used to implement features as the following:

+   * Access limits—Limit access to long-distance calls to certain telephones.
* Routing—Route calls based on their extensions.
* Autoanswatt—Set up automated greeting with message prompts.
* Menus—Set up automated menus for different departments.
* Authentication—Require passwords to access certain extensions.
* Callback—Return calls to route through the presumably cheaper Asterisk system.
* Privacy—Create blacklists for unwanted calls.
* PBX multihosting—Configure multiple PBXs on the same Asterisk server.
* Daytime/nighttime—Set up different actions at different hours
* Macros—Create scripts for different functions.

These features are described at http://www.voip-info.org/. While there are too many configuration files in the /etc/asterisk/ directory to detail in this section, they do include features from A to Z. For example, the ads.conf file specifies the analog display services interface ADSI associated with messages on the small screens included with many common business telephones. The zaptel.conf file configures a telephony hardware driver application programming interface (API), now known as the Digium Asterisk Hardware Device Interface (DAHDI).

# Security Risks with Asterisk

When configuring Asterisk, you need to be aware of the legal responsibility associated with telephone systems. While such laws vary by jurisdiction, in general, you should not configure spoofing of other telephone numbers, you should not overload or otherwise disrupt service on other telephone networks, and you should not use Asterisk to intercept calls from other users.

Naturally, as a security professional, you need to make sure that these situations do not arise on your systems.

# Denial of Service on Asterisk

Asterisk is different from other services in that it can support multiple connections between the same two IP addresses. And you want such connections, to enable multiple users from one company to talk with multiple users on another company simultaneously. So the rules that you create to prevent denial of service (DoS) attacks on Linux are somewhat different from those associated with the standard service.