PASSWORD FROM USERS

```
WHERE USERNAME = 'OTW' OR 1=1-- AND PASSWORD = 'anything'
```

When the database evaluates this statement, USERNAME=‘OTW’ is TRUE. Furhtermore, 1=1 also always evaluates to true. Everything after the -- (in green) is seen as a comment and ignored by the SQL interpreter, so that statement evaluates to TRUE, and you are authencicated without even using a password!

The more you know about SQL, the more effective you can be with SQL injection. We are making use of standard SQL commands and characters that make the database do what WE want. Some of the key SQL

injection characters include: Character Description

+   - ;
- Statement termination ‘ or “
- Character string indicators -- or #
- Single line comment /\*...\*/
- Multiple line comment +
- Addition or concatenation ||
- concatenate