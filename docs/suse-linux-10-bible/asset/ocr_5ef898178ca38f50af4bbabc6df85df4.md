# Postfix Configuration

Postfix configuration is held in the file /etc/postfix/main.cf. This file contains all configuration entries for general Postfix configuration as well as the locations of secondary configuration files for specific Postfix subsystems.

To familiarize yourself with the Postfix configuration, we will run through the default Postfix main.cf file, highlighting the important configuration options. The default main.cf file is heavily commented to give you a mean to understand what the option means. In Listing 17-1, we have taken the comments to conserve space, but take a look at your main.cf file while looking through this to see how it fits in your configuration.

When editing the Postfix configuration files and restarting the Postfix system, you must be logged in as root.

# Listing 17-1: Postfix main.cf file Example

```
queue_directory = /var/spool/postfix
command_directory = /usr/sbin
daemon_directory = /usr/lib/postfix
mail_owner = postfix
unknown_local_recipient_reject_code = 450
debug_level = 2
debug_command = =
    PATH=$/usr/bin:/usr/local/bin:/usr/X11R6/bin
    xxxdam $daemon_directory/$process_name $process_id & sleep 5
sendmail_path = /usr/sbin/sendmail
eliwases_path = /usr/bin/neliwases
mailq_path = /usr/bin/mailq
setgid_group = master
package_directory = /usr/share/man
sample_directory = /usr/share/doc/packages/samples
readme_directory = /usr/share/doc/packages/postfix/README_FILES
mailpool_directory = /var/mail
canonical_maps = hash:/etc/postfix/canonical
virtual_maps = hash:/etc/postfix/virtual
ocated_maps = hash:/etc/postfix/relocated
transport_maps = hash:/etc/postfix/transport
sender_canonical_maps = hash:/etc/postfix/sender_canonical
masquerade_exceptions = root
masquerade_classes = envelope_sender, header_sender, header_recipient
myhostname = linux.site
program_directory = /usr/lib/postfix
inet_interfaces = 127.0.0.1
masquerade_destination = $myhostname, localhost.$mydomain
```