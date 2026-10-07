Sendmail cleans up a file as it is reading. You should present Sendmail with files that are already clean and properly formatted. Doing otherwise confuses the other system administrators who might be called in to maintain your system and introduces the possibility that you will create a bad scanf pattern that can be exploited by an intruder in a buffer-overflow attack.

> NOTE scanf is a C library routine. C programming and the details of scanf are beyond the scope of this book. For more information, see The Programming Language by Brian Kernighan and Dennis Ritchie (Prentice Hall, 1988).

The second F command in Listing 7.5 loads class R from the file /etc/mail/relay-domains. You'll recall from Chapter 6, class R holds the names of domains for which Sendmail will relay mail and the relay-domains file is the traditional way to load values into class R. The -o switch is that the -o switch is switched before the pathname. Notice that the local-hosts file used in the first F command has the -o switch and therefore is mandatory. This is why we get the error “cannot open /etc/mail/local-hosts” in Listing 4.2 of Chapter 4 (“Creating a Basic Sendmail Configuration”) when we tried to use the generic-linux.cf configuration without a local-hosts file, we got no complaint at all about the fact that we didn't have a relay-domains file. The -o switch is very useful because it creates a more forgiving configuration that works in a variety of situations.

While the -o switch is the only switch available with the F command, the K command, our next topic, has several switch values. The K command is the most complex command used in the Local Info section. It needs to be. Unlike the F command that works with simple flat files, the K command deals with true database files.

# The Keyed File Command

The last of the four commands from the Local Info section is the K command, which defines a Sendmail database’s characteristics for the sendmail.cf file. The K command has the most complex syntax of any command in the Local Info section. The basic format of a K command is:

+   K name switches path

The various pieces of the command are separated by white space, although the white space between K and name is optional and rarely used. K, of course, is the command. name is used inside sendmail.cf to reference this database. The name can be any text string you want, but the name should be logical, such as the external filename of the database.