| %u | Numerical day of the week: Sunday = 0 |
| %U | Week number; Monday as first day of week |
| %x | Date format: 11/19/94 |
| %X | Time format: 21:05:57 |
| %y | Year (two digits) |
| %Y | Year (four digits) |
| %z | Time zone in ASCII, such as PST |
| echo | Displays any one of the include variables, listed here. Times are displayed in the time format specified by timefmt. The variable to be displayed is indicated with the var attribute. |
| DATE_GMT | Current date in Greenwich Mean Time. |
| DATE_LOCAL | Current date in the local time zone. |
| DOCUMENT_NAME | The filename (excluding directories) of the document requested by the user. |
| DOCUMENT_URL | The (%-decoded) URL path of the document requested by the user. Note that in the case of nested include files, this is not the URL for the current document. |
| LAST_MODIFIED | The last fileication date of the document requested by the user. |
| exec | Executes a shell command or a CGI program, depending on the parameters provided. Valid attributes are cgi and cmd. |
| cgi | The URL of a CGI program to be executed. The URL needs to be a local CGI, not one located on another machine. The CGI program is passed the QUERY_STRING and PATH_INFO that were originally passed to the requested document, so the URL specified cannot contain this information. You should really use include virtual instead of this directive. |
| cmd | A shell command to be executed. The results will be displayed on the HTML page. |
| fsize | Displays the size of a file specified by either the file or virtual attribute. Size is displayed as specified with the sizemnt directive. |
| file | The path (filesystem path) to a file, either relative to the root if the value starts with / or relative to the current directory if not. |
| virtual | The relative URL path to a file. |
| flastmod | Displays the last modified date of a file. The desired file is specified as with the fsize directive. |