A **Directory** block begins with a **<Directory pathname>** directive, where *pathname* is the directory to be configured. The ending directive uses the same **</>** symbols, but with the slash preceding the word "Directory": **</Directory>**. Directives placed within this block apply only to the specified directory. The following example denies access to only the **mypics** directory by requests from **www.myvids.com**.

```
<Directory /var/www/html/mypics>
Order Deny,Allow
Deny from www.myvids.com
</Directory>
```

With the **Options** directive, you can enable certain features in a directory, such as the use of symbolic links, automatic indexing, execution of CGI scripts, and content negotiation. The default is the **All** option, which turns on all features except content negotiation (**Multiviews**). The following example enables automatic indexing (**Indexes**), symbolic links (**FollowSymLinks**), and content negotiation (**Multiviews**).

```
Options Indexes FollowSymLinks Multiviews
```

Configurations made by directives in main configuration files or in upper-level directories are inherited by lower-level directories. Directives for a particular directory held in **.htaccess** files and **Directory** blocks can be allowed to override those configurations. This capability can be controlled by the **AllowOverride** directive. With the **all** argument, **.htaccess** files can override any previous configurations. The **none** argument disallows overrides, effectively disabling the **.htaccess** file. You can further control the override of specific groups of directives. **AuthConfig** enables use of authorization directives, **FileInfo** is for type directives, **Indexes** is for indexing directives, **Limit** is for access control directives, and **Options** is for the **options** directive.

```
AllowOverride all
```

# Access Control

With access control directives, such as **allow** and **deny**, you can control access to your Web site by remote users and hosts. Access control directives are listed in Table 22-6. The **allow** directive followed by a list of hostnames restricts access to only those hosts. The **deny** directive with a list of hostnames denies access by those systems. The argument **all** applies the directive to all hosts. The **order** directive specifies in what order the access control directives are to be applied. Other access control directives, such as **require**, can establish authentication controls, requiring users to log in. The access control directives can be used globally to control access to the entire site or placed within **Directory** directives to control access to individual directives. In the following example, all users are allowed access:

```
order allow,deny
allow from all
```

Table 22-6: Access Control Directives (continued)

| Directive | Description |
|---|---|
| deny from host host ... | Determines hosts that can access a given directory: all, or partial or full domain name or IP address. |
| allow from host host ... | Determines which hosts can access a given directory: all, partial, or full domain name, or IP address. |