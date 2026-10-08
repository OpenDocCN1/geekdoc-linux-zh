# ldapmodify, ldapadd 649

Specify the number of LDAP connections ldapadd or ldapmodify opens to process the modifications in the directory. The default is one connection.

-r Replace existing value with the specified value (the default for ldapmodify). When you call ldapadd or if you specify the -a option, the -r option is ignored.

-v Use verbose mode, and write diagnostics to standard output.

-w password Use password as the password for authentication to the directory.

# Examples

The format of the content of file (or standard input if you specify no -f option) is shown in the following examples.

The file /tmp/entrymods contains the following modification instructions:
dn: cnModify Me, o=XYZ, c=US
changetype: modify
replace: mail
mail: modme@atlanta.xyz.com

add: title
title: System Manager

add: jpegPhoto
jpegPhoto: /tmp/modme.jpeg

delete: description

The following command modifies the Modify Me entry as described below.
castle@ldapmodify -r -f /tmp/entrymods

+   1. Replace the current value of the mail attribute with the value
modme@atlanta.xyz.com.
2. Add a title attribute with the value System Manager.
3. Add a jpegPhoto attribute using the contents of the file /tmp/modme.jpeg to
attribute value.
4. Remove the description attribute.

In the following example, the file /tmp/newentry contains the information for
creating a new entry:

```
dn: Ann Jones, o=XYZ, c=US
objectclass: person
cn: Ann Jones
c: Annie Jones
sn: Jones
title: Director of Research and Development
mail: ajones@londonrd.xyz.com
uid: ajones
```

The following command uses the information in the newentry file to add a new entry
for Ann Jones.