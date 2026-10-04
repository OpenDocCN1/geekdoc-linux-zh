# 13.4 VS Package

| Language | Tcl |
| Primary Site | http://www.neosoft.com |
| Original Author | Steve Wahle |
| Contact | VSdb: river@ibm.net, Rick Enos |
| Tcl Revision Supported | Tcl: 7.3-7.6 Tk: 3.6-4.2 |

There are three utilities in the VS suite.

+   - VSdb A small database package.
- VSform A forms-based GUI generator.
- VSrpt A report-generating package.

These packages are written in pure Tcl and can be easily merged into an application. You can use one or all of the packages; they do not require each other. The VSform package, as a stand-alone, is a good tool for creating forms-based graphical interfaces to older pieces of code, and the VSdb package is fine for personal or small business database requirements.
The packages are documented with README files and short examples.

The next example creates an address book database. It supports adding entries to the database and can search on substrings in the name field.

# VSdb and VSform Example

# Example Script

```
source TclVSdb.tcl
source TkVSform.tcl
```

```
#
# Database access procedures that will be invoked by the buttons.
#
```