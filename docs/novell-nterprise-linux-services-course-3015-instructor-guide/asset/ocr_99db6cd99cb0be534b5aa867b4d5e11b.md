List User objects represent the members of a list. When users subscribe to a list, a List User is added to the respective Mailing List object.

You can also add list members by creating List User objects within the Mailing List object.

# NDS Mailing Lists

NDS mailing lists allow you to send messages to eDirectory users.

Unlike Mailing Lists, NDS Mailing Lists are made up of eDirectory objects rather than user email addresses. Selected eDirectory objects can include

+   - Container objects
+   - Groups
+   - Organizational roles
+   - Aliases
+   - User objects

If a container object is selected, messages are forwarded to the users within the designated Container object.

# Mailing Lists Container

The Mailing Lists container is created in the Internet Services container during installation. This container holds all of the messaging system's available Mailing List objects.

The List Agent references the Mailing Lists container when scanning the message queue for messages addressed to mailing lists.