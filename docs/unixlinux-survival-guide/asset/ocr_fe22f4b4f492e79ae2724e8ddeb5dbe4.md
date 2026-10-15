# 6.2.1 Tools for Documentation

The smallest entity with regard to documentation is a plain text file. As long as this file does not contain too much information, applying a simple structure will be sufficient. This is not about XML here: headlines, paragraphs, indentation, and enough room between the entries should provide the means to structure the information. Creating such documents, using any text editor capable of saving plain ASCII, is more or less what every system administrator does while editing configuration files, anyway. You should use the program you feel comfortable with. You just have to make sure to save the files either in plain ASCII or at least a format readable by as many programs as possible. If there is a well-formed directory tree thrown in the mix—a tree structure, to be precise—everything starts falling into place.

In other words you could make use of the operating system’s capability to create hierarchies by nesting directories to create the structure for storing the documents. If you want to create a structure to represent the array of servers, for example, you can use the following approach. The top-level directory is named after the network or branch of network that houses the servers, the next level contains directories named after the servers and directories named after procedures to be followed, schemes that need documenting, etc. Listing 6.1 shows a possible structure.

# LISTING 6.1 Directory Structure to Document Servers

```
servers
    policies
        security
            mail.txt
            firewall.txt
            access.txt
            ...
    common_files
        hosts
        resolv.conf
        nsswitch.conf
        ...
    mailserver
        hardware_description.txt
        IP_config.txt
        applied_patches.txt
        ...
    fileserver_org
    fileserver_admin
    ...
```