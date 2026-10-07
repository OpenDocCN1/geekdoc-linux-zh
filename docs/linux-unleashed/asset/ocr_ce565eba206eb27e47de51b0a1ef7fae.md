Note that these ignore statements only work with file extensions. To be more broad, you can use wildcards and the keyword ignore_patt (for ignore pattern). For example, the line:

```
ignore_patt: ^usr$
```

ignores any file with the letters usr at the beginning of the name.

# The gopherlocal.conf File

In the file gopherlocal.conf, you have to make two small changes to identify the system administrator, otherwise your system generates many annoying notes. The lines in the gopherlocal.conf file look like this by default:

```
Admin: blank
AdminEmail: blank
```

If you do not change these entries to actual values, Gopher can generate all kinds of weird error messages. The Admin field usually has the administrator's name and sometimes a telephone number. For example, the file could be filled out as follows:

```
Admin: Yvonne Chow, 555-1212
AdminEmail: ychow@chattton.com
```

Another setting you should provide in the gopherlocal.conf file is the Abstract, a short description of what your particular Gopher service provides. If you don't change the default setting, users get a message prompting them to request the Abstract, so you may as well do it right away. Multiple lines in an abstract value are followed by a backslash to show the continuation. A sample Abstract setting looks like this:

```
Abstract: This server provides sound and graphics files \
collected by the administrator on a recent trip to Outer \
Mongolia.
```

General information about your site is provided with a number of general settings for the site name, the organization that runs the site, your machine's geographic location, the latitude and longitude of your site, and a time zone setting. You can leave these blank if you want, but providing the information leads to a more complete Gopher site. The settings in a sample gopherlocal.conf file look like this:

```
Site: Explore_Mongolia
Org: Mongolia Tourist Bureau
Loc: North Bay, Ontario, Canada
Geog: blank
TZ: EDT
```

![](bbox=[0.85, 0.78, 0.96, 0.94])