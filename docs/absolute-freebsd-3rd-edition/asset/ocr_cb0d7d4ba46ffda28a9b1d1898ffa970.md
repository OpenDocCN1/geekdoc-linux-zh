The dataset for `/var/db` exists, but it can’t be mounted. Check the contents of your `/var/db` directory to verify everything’s still there. You can now create a dataset for `/var/db/postgres` and even `/var/db/postgresql/data96`.

```
# zfs create zroot/var/db/postgres
# zfs create zroot/var/db/postgres/data96
# chown -R postgres:postgres /var/db/postgres
```

You have a dataset for your database, and you still have the files in `/var/db` itself as part of the root dataset. Now initialize your new Postgres database and go!

As you explore ZFS, you’ll find many situations where you might want to set properties at dataset creation or use unmounted parent datasets.

# Moving Files to a New Dataset

If you need to create a new dataset for an existing directory, you’ll need to copy the files over. I recommend you create a new dataset with a slightly different name, copy the files to that dataset, rename the directory, and then rename the dataset. Here, I want a dataset for `/usr/local`, so I create it with a different name.

```
# zfs create zroot/usr/local/pgsql-new
```

Copy the files with tar(1), exactly as you would for a new UFS partition (see Chapter 11).

```
# tar cfC - /usr/local/pgsql . | tar xpfC - /usr/local/pgsql-new
```

Once it finishes, move the old directory out of the way and rename the dataset.

```
# mv /usr/local/pgsql /usr/local/pgsql-old
# zfs rename zroot/usr/local/pgsql-new zroot/usr/local/pgsql
```

My Postgres data now lives on its own dataset.