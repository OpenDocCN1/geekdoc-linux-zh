# nis+, NIS+, nis 931

+   - Link
- Entry
- Private

NIS+ Directory Object
Each NIS+ namespace has at least one NIS+ directory object. An NIS+ directory is like a UNIX file-system directory that contains other NIS+ objects, including NIS+
directories. The NIS+ directory that forms the root of the NIS+ namespace is called the root directory. NIS+ has two special directories.

+   - org_dir consists of all the system administration tables such as passwd, hosts, and mail_aliases.
- groups_dir holds NIS+ objects that are used for access control.

The collection of org_dir,groups_dir, and their parent directory is referred to as an NIS+ domain. You can arrange NIS+ in a treelike structure such that the NIS+
amespace can manage the organizational or administrative hierarchy.

# NIS+ Table Object

NIS+ tables (not files) contained within NIS+ directories store the actual information about some particular type. For example, the hosts system table stores information about the IP address of the hosts in that domain. NIS tables are multicolumn, and you can search the tables through any of the searchable columns. Each table object defines the schema for its table. The NIS+ tables consist of NIS+ entry objects. For each entry in the NIS+ table, there is an NIS+ entry object. NIS+ entry objects conform to the schema defined by the NIS+ table object.

# NIS+ Group Object

NIS+ groups are used for access control at group granularity. NIS+ group objects, contained within the groups_dir directory of a domain, contain a list of all the NIS+ principals within a certain NIS+ group. An NIS principal is a user or a machine making NIS requests.

# NIS+ Link Object

NIS+ link objects are like UNIX symbolic file-links. They are typically used for shortcuts in the NIS+ namespace.
Refer to nis_objects(3NSL) for more information about the NIS+ objects.

# NIS+ Names

The NIS+ service defines two forms of names.

+   - Simple names identify NIS+ objects contained within the NIS+ namespace.
- Indexed entries, entries within NIS+ tables are returned to the caller as NIS+ objects of entry type, NIS+ objects are implemented as a union structure that is described in the file rpcsc/nis_object.x.

The differences between the various types and the meanings of the components of these objects are described in nis_objects(3NSL).

# Simple Names

Simple names consist of a series of labels that are separated by the (dot) character. Each label is composed of printable characters from the ISO Latin-1 set. Each label can be