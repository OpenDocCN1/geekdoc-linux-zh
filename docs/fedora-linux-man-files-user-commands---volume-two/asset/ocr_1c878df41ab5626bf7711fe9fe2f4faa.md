# > EXAMPLES

The point of this helper is to reduce the number of times you must type your username or password. For example:

```
$ git config credential.helper cache $ git push Username: <type your username> Password: <type your password> [work for 5 more minutes] $ git push [your credentials are used automatically]
```

You can provide options via the credential.helper configuration variable (this example drops the cache time to 5 minutes):

```
$ git config credential.helper 'cache --timeout=300'
```