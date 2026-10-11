
If the value of `name_val` is something like `O'Malley, Brian`, the resulting statement is illegal because a quote appears inside a quoted string:

```sql
SELECT * FROM mytbl WHERE name = 'O'Malley, Brian'
```

You need to treat the inner quote specially so that the server doesn't interpret it as the end of the name. The standard SQL convention for doing this is to double the quote within the string. MySQL understands that convention, and also allows the quote to be preceded by a backslash, so you can write the statement using either of the following formats:

```sql
SELECT * FROM mytbl WHERE name = 'O''Malley, Brian'
SELECT * FROM mytbl WHERE name = 'O\'Malley, Brian'
```

To deal with this problem, use `mysql_real_escape_string()`, which encodes special characters to make them usable in quoted strings. Characters that `mysql_real_escape_string()` considers special are the null byte, single quote, double quote, backslash, newline, carriage return, and Control-Z. (The last one is special on Windows, where it often signifies end-of-file.)

When should you use `mysql_real_escape_string()`? The safest answer is "always." However, if you're sure of the format of your data and know that it's okay—perhaps because you have performed some prior validation check on it—you need not encode it. For example, if you are working with strings that you know represent legal phone numbers consisting entirely of digits and dashes, you don't need to call `mysql_real_escape_string()`. Otherwise, you probably should.

`mysql_real_escape_string()` encodes problematic characters by turning them into two-character sequences that begin with a backslash. For example, a null byte becomes `\0`, where the `0` is a printable ASCII zero, not a null. Backslash, single quote, and double quote become `\\`, `\'`, and `\"`.

To use `mysql_real_escape_string()`, invoke it like this:

```c
to_len = mysql_real_escape_string(conn, to_str, from_str, from_len);
```

`mysql_real_escape_string()` encodes `from_str` and writes the result into `to_str`. It also adds a terminating null, which is convenient because you can use the resulting string with functions such as `strcpy()`, `strlen()`, or `printf()`.

`from_str` points to a char buffer containing the string to be encoded. This string may contain anything, including binary data. `to_str` points to an existing char buffer where you want the encoded string to be written; do not pass an uninitialized or NULL pointer, expecting `mysql_real_escape_string()` to allocate space for you. The length of the buffer pointed to by `to_str` must be at least (`from_len`+2)+1 bytes long. (It's possible that every character in `from_str` will need encoding with two characters; the extra byte is for the terminating null.)

`from_len` and `to_len` are unsigned long values. `from_len` indicates the length of the data in `from_str`; it's necessary to provide the length because `from_str` may contain null bytes and cannot be treated as a null-terminated string. `to_len`, the return value from `mysql_real_escape_string()`, is the actual length of the resulting encoded string, not counting the terminating null.

When `mysql_real_escape_string()` returns, the encoded result in `to_str` can be treated as a null-terminated string because any null bytes in `from_str` are encoded as the printable `'\0'` sequence.

To rewrite the SELECT-constructing code so that it works even for name values that contain quotes, we could do something like this:

```c
char stmt_buf[1024], *p;

p = strcpy(stmt_buf, "SELECT * FROM myth WHERE name='");
p += strlen(p);
p += mysql_real_escape_string(conn, p, name_val, strlen(name_val));
*p++ = '\'';
*p++ = ';';
*p = '\0';
```

Yes, that's ugly. To simplify the code a bit, at the cost of using a second buffer, do this instead:

```c
char stmt_buf[1024], buf[1024];

(void) mysql_real_escape_string(conn, buf, name_val, strlen(name_val));
sprintf(stmt_buf, "SELECT * FROM myth WHERE name='%s'", buf);
```

It's important to make sure that the buffers you pass to `mysql_real_escape_string()` really exist. Consider the following example, which violates that principle:

```c
char *from_str = "some string";
char *to_str;
unsigned long len;

len = mysql_real_escape_string(conn, to_str, from_str, strlen(from_str));
```

What's the problem? `to_str` must point to an existing buffer, and it doesn't—it's not initialized and may point to some random location. Don't pass an uninitialized pointer as the `to_str` argument to `mysql_real_escape_string()` unless you want it to stomp merrily all over some random piece of memory.

### 7.4.7.2 Working with Binary Data

Another problematic situation involves the use of arbitrary binary data in a statement. This happens, for example, in applications that store images in a database. Because a binary value may contain any character (including null bytes, quotes, or backslashes), it cannot be considered safe to put into a statement as is.

`mysql_real_escape_string()` is essential for working with binary data. This section shows how to do so, using image data read from a file. The discussion applies to any other form of binary data as well.

Suppose that you want to read images from files and store them in a table named `picture`, along with a unique identifier. The MEDIUMBLOB type is a good choice for binary values less than 16MB in size, so you could use a table specification like this:

```sql
CREATE TABLE picture
(
  pict_id   INT NOT NULL PRIMARY KEY,
  pict_data MEDIUMBLOB
);
```

To actually get an image from a file into the `picture` table, the following function, `load_image()`, does the job, given an identifier number and a pointer to an open file containing the image data:

```c
int
load_image (MySQL *conn, int id, FILE *f)
{
  char        stmc_buf[1024*1024], buf[1024*10], *p;
  unsigned long from_len;
  int           status;

  /* begin creating an INSERT statement, adding the id value */
  sprintf (stmc_buf,
           "INSERT INTO picture (pict_id,pict_data) VALUES (%d,'",
           id);
  p = stmc_buf + strlen (stmc_buf);
  /* read data from file in chunks, encode each */
  /* chunk, and add to end of statement */
  while ((from_len = fread (buf, 1, sizeof (buf), f)) > 0)
  {
    /* don't overrun end of statement buffer! */
    if (p + (2*from_len) * 3 > stmc_buf + sizeof (stmc_buf))
    {
      print_error (NULL, "image is too big");
      return (1);
    }
    p += mysql_real_escape_string (conn, p, buf, from_len);
  }
  *p++ = '\'';
  *p++ = ')';
  status = mysql_real_query (conn, stmc_buf, (unsigned long) (p - stmc_buf));
  return (status);
}
```

`load_image()` doesn't allocate a very large statement buffer (1MB), so it works only for relatively small images. In a real-world application, you might allocate the buffer dynamically based on the size of the image file.

Getting an image value (or any binary value) back out of a database isn't nearly as much of a problem as putting it in to begin with. The data value is available in raw form in the MYSQL_ROW variable, and the length is available by calling `mysqli_fetch_lengths()`. Just be sure to treat the value as a counted string, not as a null-terminated string.

## 7.5 An Interactive Statement-Execution Program

We are now in a position to put together much of what we've developed so far and use it to write a simple interactive statement-execution client, `exec_stmt.c`. This program lets you enter statements, executes them using our general-purpose statement handler `process_statement()`, and displays the results using the `process_result_set()` display formatter developed in the preceding section.

`exec_stmt` is similar in some ways to `mysqli`, although of course with not as many features. There are several restrictions on what `exec_stmt` will allow as input:

- Each input line must contain a single complete statement.
- Statements should not be terminated by a semicolon or by `\g`.
- The only non-SQL commands that are recognized are `quit` and `\q`, which terminate the program. You can also use Ctrl-D to quit.

It turns out that `exec_stmt` is almost completely trivial to write (about a dozen lines of new code). Almost everything we need is provided by our client program skeleton (`connect2.c`) and by other functions that we have written already. The only thing we need to add is a loop that collects input lines and executes them.

To construct `exec_stmt`, begin by copying the client skeleton `connect2.c` to `exec_stmt.c`. Then add to that the code for the `process_statement()`, `process_result_set()`, and `print_dashes()` functions. Finally, in `exec_stmt.c`, look for the line in `main()` that says this:

```c
/* ... issue statements and process results here ... */
```

Replace that line with this while loop:

```c
while (1)
{
  char  buf[10000];

  fprintf (stderr, "query> ");            /* print prompt */
  if (fgets (buf, sizeof (buf), stdin) == NULL) /* read statement */
    break;
  if (strcmp (buf, "quit\n") == 0 || strcmp (buf, "\\q\n") == 0)
    break;                                /* execute it */
  process_statement (conn, buf);
}
```

Compile `exec_stmt.c` to produce `exec_stmt.o`, link `exec_stmt.o` with the client library to produce `exec_stmt`, and you're done. You have an interactive MySQL client
