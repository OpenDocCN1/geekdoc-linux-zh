# TABLE 24-3 (continued)

| Short Name | Long Name | Description |
| --- | --- | --- |
| -l | --list | Display a list of available databases on the server and exit. |
| -o | --output | Redirect query output to the specified file. |
| -p | --post-post | Specify the PostgreSQL server TCP port to connect with. |
| -P | --pset | Set the table printing option specified to a specified value. |
| -q | --quiet | Quiet mode, doesn't display output messages. |
| -R | --record-separator | Use the specified character as the record separator. The default is the newline character. |
| -s | --single-step | Prompt to continue or cancel after every SQL query. |
| -S | --single-line | Specify that the Enter key defines the end of an SQL query instead of a semicolon. |
| -t | --tuples-only | Disable column headers and footers in table output. |
| -T | --table-attr | Use the HTML tag specified when in HTML mode. |
| -U | --username | Use the specified user name to connect to the PostgreSQL server. |
| -v | --variable | Set the specified variable to a specified value. |
| -V | --version | Display the psql version number and exit. |
| -W | --password | Force a password prompt. |
| -x | --expanded | Enable table output to display additional information for records. |
| -X | --nopsqlrc | Don't process the psql startup file. |
| ? | --help | Display the psql command line help and exit. |

As mentioned in the previous section, the administrative account for PostgreSQL is called postgres. Since PostgreSQL uses Linux user accounts to validate users, you must be logged in as the postgres Linux account to access the PostgreSQL server as the postgres user.

Since the postgres user account is a special account, you shouldn't assign a password to it That way no one can try to break into the system using that account.