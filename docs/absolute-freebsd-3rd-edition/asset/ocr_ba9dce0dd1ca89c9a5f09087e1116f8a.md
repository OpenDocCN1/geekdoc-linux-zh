The `/etc/login.access` file has three colon-delimited fields. The first either grants (+) or denies (-) the right to log in; the second is a list of users or groups; and the third is a list of connection sources. You can use an `ALL` or `ALL EXCEPT` syntax, which allows you to make simple but expressive rules. Rules are checked on a first-fit basis. When `login(1)` finds a rule where the user and the connection source match, the connection is immediately accepted or rejected, making rule order vital. The default is to allow logins.

For example, to allow only members of the wheel group to log in from the system console, you might try this rule:

```
``` 
+:wheel:console 
```
```

The problem with this rule, however, is that it doesn’t actually deny users login privileges. Since the default is to accept logins, and since all this rule does is explicitly grant login privileges to the users in the wheel group, nothing changes. Bert certainly isn’t in the wheel group, but if he tries to log in, no rule denies him access.

You could try two rules like this:

```
``` 
+:wheel: console 
-:ALL:console 
```
```

This set of rules would achieve the desired effect but is longer than you need. Use `ALL EXCEPT` instead.

```
``` 
-:ALL EXCEPT wheel: console 
```
```

This rule rejects unwanted logins most quickly and runs less risk of administrator error. As a rule, it’s best to build `login.access` lists by rejecting logins, rather than permitting them. FreeBSD immediately rejects nonwheel users at the console upon hitting this rule.

Change the default from “allow access” to “deny access” by adding a final rule.

```
``` 
-:ALL:ALL 
```
```