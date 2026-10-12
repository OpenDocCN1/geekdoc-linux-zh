# 17.8 LDAP – directories and database considerations

What is an LDAP “directory”? The concept of a directory evolved from things like phone directories – a list of people, and information relating to each of them, in a specific order so that the directory can be searched to find the information needed. An LDAP directory contains information (with a specification of what type of data it is), in a particular order (like the phone book) so it can be searched or browsed, e.g.

+   – I want Fred Bloggs’ *e*-mail address
+   
+   – list all *e*-mail addresses containing Bloggs
+   
+   – is there a color printer on the LAN near me?

An LDAP directory is made up of *entries*. An entry is a collection of *attributes*. Each attribute has a type and one or more values. The type specifies whether single or multiple values are allowed, and what the format of the data is. For example, a phone number attribute would probably allow multiple values, a surname attribute has a text-string value, and a **photoID** attribute might contain a GIF image as a binary object.

Entries are stored in a hierarchy in the directory, just like files are stored in a hierarchy on a disk. Each entry’s full name, its *distinguished name* (DN), is made up of the name of this node in the *directory information tree* (DIT), followed by the names of all its parent nodes. All DNs are unique, so any entry can be specified unambiguously. For example, in a directory ordered by “common name” within organization unit (i.e. department) within organization within country, an entry might be

cn=Niall Mansfield, ou=R&D, o=UIT Cambridge, c=GB

Directories in the LDAP sense are quite general and can contain almost any information, although:

+   – they are still most often used for user-related information – usernames, passwords (which can be encrypted), phone numbers, public encryption keys, etc.
+   
+   – they contain information that is structured in some way, and is searchable (e.g. by username or by *e*-mail address)
+   
+   – they are not suited for information that is not structured and searchable
+   
+   – directories are used almost entirely for lookups rather than updates (reading as opposed to writing) and are optimized for this, so that, for example, looking up an *e*-mail address for someone is very fast. Some LDAP directories don’t implement elaborate transaction-oriented database operations for updates because they occur so rarely.

Because LDAP is a network service, the directory can be used from outside your LAN. (You should make sure suitable security mechanisms are in place, of course. Even internally, access control and data encryption are needed both to prevent unauthorized changes, and to preserve confidentiality, e.g. of personal details or passwords.) This allows a large organization to maintain a single, organization-wide user database for access control, per-user application data, etc. This simplifies what have historically been the awkward problems of user management: