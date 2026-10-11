# 12.4  Managing MySQL User Accounts

635

```
[REQUIRE encryption requirements] [WITH grant_or_resource_management_options];
```

If the named account exists, GRANT modifies its privileges. If the account does not ex-ist, GRANT creates it with the given privileges. To avoid the possibility of GRANT creating a new account that has no password (and thus is insecure), enable the NO\_AUTO\_CREATE\_USER SQL mode. This mode is available as of MySQL 5.0.2 and pre-vents GRANT from creating the account unless an IDENTIFIED BY clause is present.

Several of these clauses are optional and need not be specified at all. In general, you'll most commonly use the following parts:

+   * privileges indicates the privileges to assign to the account. For example, the SELECT privilege enables a user to issue SELECT statements and the SHUTDOWN privilege enables the user to shut down the server. Multiple privileges can be named, separated by commas.

+   * columns indicates the columns to which a privilege applies, separated by commas and listed within parentheses. This is optional, and you use it only to set up column-specific privileges. The column list must follow the name of each privilege to which it applies.

+   * what indicates the level at which the privileges apply. The most powerful level is the global level, for which any given privilege applies to all databases and all tables. Global privileges can be thought of as superuser privileges. Privileges also can be made database-specific, table-specific, column-specific (if you specify a columns clause), or routine-specific.

+   * account indicates which account is being granted the privileges. The account format is `user_name'@'host_name`, as described in Section 12.4.1.1, “Specifying Account Names.”

+   * password indicates the password to assign to the account. This is optional and is unnecessary if the account already exists and has a password. If you include the IDENTIFIED BY clause for an existing account, the new password replaces the current one. As with CREATE USER, when you do use IDENTIFIED BY, the password value should be the literal text of the password. GRANT will encode the password for you; don't use the PASSWORD() function.

The REQUIRE and WITH clauses are optional. REQUIRE is used for setting up accounts that must connect over secure connections using SSL. WITH is used to grant the GRANT OPTION privilege that enables the account to give its own privileges to other users. WITH also is used to specify resource management options that enable you to place limits on how many connections or statements an account can use per hour. These options help you prevent the account from hogging the server.