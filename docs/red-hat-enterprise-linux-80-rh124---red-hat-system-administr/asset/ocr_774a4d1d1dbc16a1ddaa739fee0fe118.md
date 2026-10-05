# REGISTERING SYSTEMS FOR RED HAT SUPPORT

# OBJECTIVES

After completing this section, you should be able to register a system to your Red Hat account and assign it entitlements for software updates and services using Red Hat Subscription Management.

# RED HAT SUBSCRIPTION MANAGEMENT

Red Hat Subscription Management provides tools that can be used to enable entities to product subscriptions, allowing administrators to get updates to software packages and track information about contracts and subscriptions used by the systems. Standard tools such as PackageKit and yum can obtain software packages and updates through a content distribution network, provided by Red Hat.

There are four tasks performed with Red Hat Subscription Management tools:

+   - Register a system to associate that system to a Red Hat account. This allows Subscription Manager to uniquely inventory the system. When no longer in use, a system may be unregistered.
- Subscribe a system to entitle it for updates for Red Hat products. Subscriptions have specific levels of support, expiration dates, and default repositories. The tools can be used to either auto-attach or select a specific entitlement. As needs change, subscriptions may be removed.
- Enable repositories to provide software packages. Multiple repositories are enabled by default with each subscription, but other repositories such as updates or source code can be enabled as needed.
- Review and track entitlements that are available or consumed. Subscription information can be viewed locally on a specific system or, for an account, in either the Red Hat Customer Portal Subscriptions page or the Subscription Asset Manager (SAM).

# Registering a System

There are a number of different ways to register a system with Red Hat Customer Portal. There is a graphical interface that you can use with a GNOME application or the Web Console service, and there is a command-line tool.

To register a system with the GNOME application, launch Red Hat Subscription Manager by selecting Activities. Type subscription in the Type to search... and click on Red Hat Subscription Manager. Enter the appropriate password when prompted to authenticate. This displays the Subscriptions window.