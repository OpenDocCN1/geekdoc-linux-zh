
## nis+, NIS+, nis

be of any non-zero length provided that the fully qualified name is fewer than NIS_MAXNAMELEN octets including the separating dots. (See rpcsvc/nis.h for the actual value of NIS_Grammar in the current release.) Labels that contain special characters (see "Grammar") on page 932 must be quoted. The NIS+ namespace is organized as a singly rooted tree. Simple names identify nodes within this tree. These names are constructed so that the leftmost label of the leaf identify the parent node of the object. all the labels to the leaf's directory. The leaf directory is a naming directory and should not be confused with a file-system directory.

For example, the name example.simple.name is a simple name with three labels, where example is the leaf node in the directory. This leaf is simple.name, which by itself is a simple name, the leaf of is simple, and its directory is simply name.

The function nis_leaf_of(name) returns the first label of a simple name. The function nis_domain_of(SNL) returns the name of the directory that contains the leaf. Iterative use of these two functions can break a simple name into each of its label components.

The name dot (.) is reserved to the global root of the namespace. For systems that are connected to the Internet, this global root is served by a Domain Name Service. When NIS+ server is serving a root directory whose name is not dot (), this is referred to as a local root.

NIS names are said to be fully qualified when the name includes all the labels identifying all of the directories, up to the global root. Names without the trailing dot are called partially qualified.

## Indexed Names

```
[column_name=value, column_name=value, ...]
```

A search is combined with a simple name to form an indexed name by concatenating the two parts, separated by a comma as follows
[search-criteria], table, directory.

When multiple name/value pairs are present in the search criteria, only those entries in the table that have the appropriate value in all columns are returned. When no column name/value pairs are specified in the search criteria, [], all entries are in the table returned.

## Grammar

The following text represents a context-free grammar that defines the set of legal NIS+ names. The terminals in this grammar are the characters dot (.), open bracket ([), comma (,), equal (=), and white space. Use the vertical bar (|) character to separate alternate productions. Read this syntax as this production OR this

```
name ::= simple-name | indexed-name
simple-name ::= string.string.simple-name
```

## nis+, NIS+, nis

```
indexed-name ::= search-criteria, simple-name
search-criteria ::= (attribute-list)
attribute-list ::= attribute | attribute, attribute-list
attribute ::= string = string
string ::= ISO Latin-1 character set except the character slash (/).
The initial character cannot be a terminal character or t at (@), plus (+), or dash (-).
```

Terminals that appear in strings must be quoted with double quote ("). You can quote the character by quoting it with itself ("").

## Name Expansion

The NIS+ service accepts only fully qualified names. However, because such names can unwind, the NIS+ names in section 1 use a set of standard expansion rules to fulfill a partially qualified name. This expansion is actually done by the NIS+ library function nis_getnames(3), which generates a list of names by using the directory search path or the NIS_PATH environment variable.

The NIS+ directory search path includes all the names in its path. nis_getnames() is invoked by the functions nis_lookup(3) and nis_list(3) when the EXP_NAME flag is used.

The NIS_PATH variable contains an ordered list of simple names. The names are separated by the colon (:). If any name in the list contains colons, the should be quoted as described in the Grammar section. When the list is exhausted, the resolution function returns the error NIS_NOTFOUND. This error message masks the fact that the name existed but for it was unreachable. If the name presented to the list or lookup interface is fully qualified, the EXPAND_NAME flag is ignored. In the list of names from the NIS_PATH environment variable, the dollar sign ($) character is treated specially. Simple names that end with the label $ has this character replaced by the default directory (nis_local_directory(3)). Using $ as a name in this list results in name being replaced by the list of directories between the default directory and the global root that contain at least two labels.

Below is an example of this expansion. With a default directory of some.long.domain.name and the NIS_PATH variable set to fed.org.dir.$, the path initially broken up into the following list:

- 1. fed.bar.
- 2. org_dir.some.long.domain.name.
- 3a some.long.domain.name.
- 3b long.domain.name.
- 3c domain.name.

The dollar sign in the second component is replaced with the default directory. The dollar sign in the third component is replaced with the list of directories between the default directory and the global root that have at least two labels in them. effective path becomes:

## nis+, NIS+, nis

Each of these simple names is appended to the partially qualified name that was passed to the nis_lookup(3) or nis_list(3) interface. Each is tried until NIS_SUCCESS is returned or the list is exhausted.

If the NIS_PATH variable is not set, the path $ is used.

The library function nis_getname(3) can be called from user programs to generate the list of names that would be attempted. The program nisdefaults(1) with the -s option can also be used to show the fully expanded path.

## Concatenation Path

Normally, all the entries for a certain type of information are stored within the table itself. However, at times it is desirable for the table to point to other tables where entries can be found. For example, you may want to store all the IP addresses in the host table for their own domain and want to be able to resolve hosts in some other domain without explicitly specifying the new name. NIS+ provides a mechanism for concatenating different but related tables with NIS+ concatenation path. With a concatenation path, you can create a sort of flat names from a hierarchical structure. You can also create a table with no entries and just point the hosts or any other table to its parent domain. Note that with such setup, you are moving the administrative burden of managing names to the parent domain. The concatenation path slows the request response time more tables and servers are searched. It also decreases the availability of tables if all the servers are incapacitated for a particular directory in the table.

The NIS+ concatenation path is also referred to as the table path. This path is set up at creation time with nisbind(1). You can specify more than one table to be concatenated, and the tables are searched in the given order. Note that the NIS+ client libraries, by default, do not follow the concatenation path set in site-specific tables. Refer to nis_list(3) for more details.

## Namespaces

The NIS+ service defines two additional disjoint namespaces for its own use are:

- The NIS+ principal namespace.
- The NIS+ group namespace.

The names associated with the group and principal namespaces are syntactically identical to simple names. However, the information they represent cannot be obtained by direct presentation of these names to the NIS+ interfaces. Instead, special interfaces are defined to map these names into NIS+ names so that they can be resolved.

## Principal Names

NIS+ names are used to uniquely identify users and machines that are making NIS+ requests. These names have the following form:

principal.domain

Here, domain is the fully qualified name of an NIS+ directory where the principal's credentials can be found. See "Directories and Domains" on page 936 for more information on domains. Note that this name, principal, is not a leaf in the NIS+ namespace.

Credentials are used to map the identity of a host or user from one context, such as a process UID, into the NIS+ context. They are stored as records in an NIS+ named cred, which always appears in the org_dir subdirectory of the name in
