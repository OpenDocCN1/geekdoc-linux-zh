The container-specific message store is the directory where the mailboxes for users in the current container are located. This does not affect the general message queue and SCMS directories, which will always be located in the default message store directory.

If configured, container domains appear in the From field of user messages and are referenced by the Address Book Agent in returning users' address book information. Container domains do not allow you to have non-unique user IDs in different containers.

# User Objects

The NetMail attributes added to User objects replicate many of the user configuration options available in the Modular Web client, including privacy level, forward and autoreply messages, and proxy configuration.

Providing the user configuration options in both the User object and Modular Web client gives you the option of centrally managing these options through the User object or allowing users to self-manage these options through the Modular Web client.

The User object also replicates many of the configuration options available in Parent objects. This duplication lets you configure general settings in the Parent object, but create exceptions for individual User objects.

# How Messages Are Processed

The core function of NetMail is message processing. Every message entering your messaging system must be processed by NetMail agents.