ler. This option is the default for Windows server systems.

+   username
This user will be added or removed from the group. Any number of users can be specified.

The following example shows issuing the NET GROUP command to add the group *hp consultants*:

```
C:\ NET GROUP "hp consultants" /ADD
The request will be processed at the primary domain controller for domain
NSDNIS.
The command completed successfully.
```

Next we add the user *marty* to the group *hp consultants* on the local system:

```
C:\ NET GROUP "hp consultants" marty /ADD
The request will be processed at the primary domain controller for domain
NSDNIS.
The command completed successfully.
```

Next we add a comment to *hp consultants*:

```
C:\ NET GROUP "hp consultants" /COMMENT:"G roup For HP Consultants"
The request will be processed at the primary domain controller for domain
NSDNIS.
The command completed successfully.
```

We can now view our handiwork by looking at the information we have added associated with the group *hp consultants*: