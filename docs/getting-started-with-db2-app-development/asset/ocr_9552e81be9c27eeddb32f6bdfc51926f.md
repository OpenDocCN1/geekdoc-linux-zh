Now let’s take a look at the other table that was created, the SCHEMA_MIGRATION table. *Figure 7.22* shows the contents of this table.

![](bbox=[0.16, 0.21, 0.84, 0.395])

# Figure 7.22 –Contents of the table SCHEMA_MIGRATION

As you can see from the figure, the SCHEMA_MIGRATION table contains only one column, the VERSION column, which is used to keep track of migration version number numbers. The version number is the numerical prefix on the migration’s filename. For example, for file 20100611202808_create_books.rb, the version is 20100611202808.

The `rake db:migrate` it its simplest form will run the `up` method for all the migrations that have not yet been run. If you want a specific version, Active Record will run the required migrations (up or down) until it has reached the specified version. For example to migrate to version 20100705000000 run:

```
rake db:migrate VERSION=20100705000000
```

If this is greater than the current version, that is, it is migrating upwards; the `up` method will be invoked on all migrations up to and including 20100705000000, if it is migrating downwards, the `down` method will be invoked on all the migrations down to, but not including, 20100705000000. To rollback to the last migration, use:

```
rake db:rollback.
```

Let’s take a look now at what has been built for this application. If the WEBrick Web server is not started, use this command to start it:

```
<app_home>\bookapp> ruby script/server
```

Then enter http://localhost:3000/books in a browser. *Figure 7.23* displays the output.