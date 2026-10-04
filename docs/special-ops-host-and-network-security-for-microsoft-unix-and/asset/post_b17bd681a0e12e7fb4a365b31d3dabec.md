
Web server's document root. This ensures that even if the Web server permits directory listing, a blank page would be returned.

# Figure 11.5 An Indexable Directory Revealed

![](img/729efc56f204a2ebffb8295c3a2dfdfb_604_0.png)

## Directory Traversal

Directory traversal refers simply to navigating between directories. For the purposes of illustration, we use an MS-DOS prompt on a typical Windows 2000 machine.
You should see the following:

Microsoft Windows 2000 [Version 5.00.2195]
(C) Copyright 1985-2000 Microsoft Corp.

```
C:\>
```

My personal documents sit in my home directory, which exists several levels away from the root directory, that is C:\SensePost\users\haroon:

```
C:\
```

```
Temp
Windows
SensePost

Finances
Stuff
Office
Users
```

Haroon
Jaco
Chris
Charll
Blah
Blah2
Common Files
Program Files

If I issued the dir command within my home directory, I would see all the files within it. When dealing with directories, the period (.) and the double-period (..) represent the current directory and the parent directory, respectively. Therefore, the command dir . would effectively list the current directory, and dir .. would list the contents of the parent directory. This can be taken further. While remaining within my home directory C:\Sense\users\haroon, I would be able to list the contents of the root directory c: by issuing dir ..\.\ command. This, in a nutshell, is referred to as traversal.

Some applications serve image or other content to users depending on requested parameters. These applications fall prone to traversal attacks when the user is to prepend a period (.), double period (..), and slash (/) to their requested resource. For example, a popular Web-based mathematical program creates images based on user input data and then saves these images using random names to some directory on the hosting server. These images are then served to the user within their browser by pointing him to the newly generated URL:

```
http://www.sensepost.com/WebApplication/SENSEAPP?SENSEStoreID=SP888808189_2408042780&StoreType=image/gif
```

The problem with this is that the CGI application SENSEAPP fails to strip malicious user input and serves any document within the document tree. An entering user could further adjust the URL mentioned above, to point to:

```
http://www.sensepost.com/WebApplication/SENSEAPP?SENSEStoreID=../../../../../../etc/passwd&StoreType=image/gif
```

There, they can request a file further up in the directory hierarchy by simply traversing the directory tree. In this case, simply viewing the source of the returned page would yield the coveted passwd of the targeted Web server. Always ensure user input is stripped of possibly hostile characters!

![](img/729efc56f204a2ebffb8295c3a2dfdfb_605_0.png)

## Command Execution

It is not uncommon to find custom Web applications that execute some sort of command on the running Web server. Indeed Web-based applications exist that facilitate the administration of the remote operating system using back-end scripts with elevated privileges. The opportunities for abusing such applications are obvious, as is the author's failure to strip meta characters from the received user input.

A typical example would be an application that allowed a user to enter a $QUERYSTRING and then performed an $ls (dir) of the specified directory. Behind the scenes, the user is presented with a form that (rather surprisingly) assigns the passed variable to the $ls and passes the command + $QUERYSTRING to the shell for execution. If the user entered /temp, the effective command would be $ls /temp. So far good—let's investigate further. Problems are introduced when the user becomes a little creative with her input. Unix/Linux shell allows the user to enter multiple commands on a single line by making use of the semicolon;) or ampersand (&&) characters. Therefore, if an attacker used special characters to concatenate our original request with a second nefarious request, the resulting output could be quite devastating to our server's security. For example, if a user entered /temp & cat /etc/passwd, both commands (ls and cat) would be run. If successful, this would provide the attacker with the contents of the /etc/passwd file (before you showed your password file).

![](img/729efc56f204a2ebffb8295c3a2dfdfb_606_0.png)

The solution is to ensure that all input is sanitized and that only input that matches predefined criteria are accepted or passed further into the script. The case in the preceding paragraph, for example, could ensure that the user supplied $email is subjected to a check that accepts only alphabets, periods, hyphens, and numerics:

```
# remove chars that are not a-z A-Z @ - 0-9 or
$email =~ tr/a-zA-Z0-9\@-\.\/dc;
```

In addition to, Perl supports the running of taint mode. Taint mode, according to the PERL TAINT FAQ (http://gunther.web66.com/FAQS/taintmode.html).

## Database Query

Most applications operate by interfacing with a database. This is often done using SQL (Structured Query Language). A common task is to retrieve data based on user-supplied criteria. For example, a login page might take a username and password and execute a query like:

```sql
SELECT * FROM users WHERE username = 'user' AND password = 'password';
```

The vulnerability arises when the application does not properly sanitize the input. If an attacker enters something like `' OR '1'='1`, the query becomes:

```sql
SELECT * FROM users WHERE username = '' OR '1'='1' AND password = ''';
```

Since `'1'='1'` is always true, the query may return all rows in the users table, potentially allowing the attacker to log in without a valid password. This is known as a SQL injection attack.

To prevent SQL injection, developers should use prepared statements or parameterized queries. These methods ensure that user input is treated as data, not as executable code.

Example of a prepared statement in PHP using PDO:

```php
$stmt = $pdo->prepare('SELECT * FROM users WHERE username = :username AND password = :password');
$stmt->execute(['username' => $username, 'password' => $password]);
$user = $stmt->fetch();
```

By using prepared statements, the database engine pre-compiles the SQL query, and the user input is bound to parameters. This makes it impossible for an attacker to alter the query's structure.

## Cross-Site Scripting (XSS)

Another common vulnerability is Cross-Site Scripting (XSS). This occurs when an application includes untrusted data in a web page without proper validation or encoding. This allows attackers to execute scripts in the victim's browser.

There are several types of XSS:

- Reflected XSS: The malicious script is reflected off the web server to the victim's browser via a URL parameter.
- Stored XSS: The malicious script is permanently stored on the server (e.g., in a database, comment field, or user profile).
- DOM-based XSS: The vulnerability exists in the client-side code rather than the server-side.

To prevent XSS, developers should encode all user-supplied data before rendering it in the browser. This means converting characters like `<` and `>` into their HTML entity equivalents (e.g., `&lt;` and `&gt;`).

Example of encoding in PHP:

```php
echo htmlspecialchars($_GET['name'], ENT_QUOTES, 'UTF-8');
```

By using `htmlspecialchars()`, any script tags provided by the user will be displayed as text rather than executed by the browser.

## Session Management Attacks

Session IDs are used to track user sessions across multiple requests. If session IDs are predictable, an attacker can hijack a user's session. This is known as session hijacking.

Common methods for session hijacking include:

- Session Sniffing: Intercepting the session ID over an unencrypted network.
- Session Prediction: Guessing the session ID based on a known pattern.
- Session Fixation: Forcing a user to use a known session ID before they log in.

To mitigrate these risks, developers should:

- Use long, random session IDs.
- Use HTTPS to encrypt all traffic.
- Set the `HttpOnly` and `Secure` flags on session cookies.
- Regenerate the session ID after login.
- Implement proper session timeouts.
