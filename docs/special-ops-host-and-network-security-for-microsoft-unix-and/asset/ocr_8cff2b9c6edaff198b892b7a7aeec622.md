# Introduction

In an enterprise environment, there are many diverse systems on the typical heterogeneous network. Often, Unix systems are a large part of the equation. In the enterprise environment, it is not uncommon to have multiple Unix systems serving specific, individual purposes. All these systems, while varying in platform and operating system type, are confronted with similar problems of default configurations and newly discovered vulnerabilities, and they require work to maintain their integrity.

We begin this chapter with a brief discussion about attacking Unix. In the first section, we examine using information gathering attacks. We follow this discussion with descriptions of common attacks used against Unix systems, such as exploiting programming errors and input validation errors.

Next we examine securely installing Unix, going through the steps necessary to obtain valid media, install the host, and configure the system to preserve host integrity. We also examine features we can use to make the host more secure, and go through the integrity verification and securing of inherited systems.

# Attacking Unix

It is impossible to determine a host to be one hundred percent secure. The best that can be done is to ensure that a host is not vulnerable to any known issues. This also includes ensuring that minimal impact will result in future compromises, and the only means of ensuring a host is reasonably secure is to attack the host.

There are two main goals of attacking Unix systems to ensure security: gaining remote access, and gaining elevated privileges locally, if required. Attacks launched by an individual are usually preceded by an information gathering attack, which we will discuss briefly.

We next look at common methods of gaining remote access to a host and then methods of gaining local privilege elevation. By the end of the section, you will have an idea of how to attack your systems using the methods in which your systems are usually attacked.

# Information Gathering Attacks

Just as an Operations Unit needs intelligence reports on a target before the launch of an attack, an intelligent attacker needs information on a site before attempting to compromise a host. An Operator would want maps, manpower, armament, and objective information before being dropped at a site to accomplish a mission; an