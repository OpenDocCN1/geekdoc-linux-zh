# 133: What is the MySQL command to create a new database called 'test'?

Answer:

```
CREATE database test;
```

# 134: What is the MySQL command to create a new user called 'test' (and password to 'password'), and give 'test' full access to the database 'test'?

Answer:

```
GRANT ALL PRIVILEGES on test.* to 'test'@'localhost'
IDENTIFIED BY 'password';
```

# 135: If Apache allows a web browser to download PHP files, instead of properly executing them, what directive is missing from the Apache configuration?

Answer:

AddHandler