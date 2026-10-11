A **class** statement enables you to define a group of users who should all be treated in the same manner. It is used in the following format:

```
class classname who
```

The arguments used in a **class** statement are listed here:

+   - **classname** —The name for this class of users
+   - **who** —One or a series of expressions that narrows down who belongs in the class

> **NOTE:** Although a **class** statement must be only one line long, if you need to extend your list of who portions, simply break them into multiple **class** statements using the same **classname** for each.

Building an expression—also referred to as a *glob*—relies on the attributes listed in Table 15.3. These are the same for anything else that refers to “globbing.”

After the initial **class** statement is:

```
email root@localhost
```

An **email** statement is much easier to follow. The argument is the email address of the person responsible for maintaining the FTP server and file space. Next is:

```
loginfails 5
```

The **loginfails** statement sets how many times a user can attempt to log in through FTP and enter a wrong username and password combination before the FTP server closes the connection to the FTP client. After this statement is a pair of **readme** statements:

```
readme README* login
readme README* cwd=*
```

# **Table 15.3** Wildcards used in glob expressions.

| Character | Purpose | Example |
| :--- | :--- | :--- |
| ? | Matches a single unspecified character | c?t matches cat and cut, but not cart |
| * | Matches any sequence of unspecified characters | c*t matches cat, cut, cart, and can't, but not cute |
| [] | Matches any of the enclosed characters | c[a-d]t matches cat but not cut |
| {} | Matches any of the comma-separated items in the list | c{ar,our}t matches cart and court, but not cut |