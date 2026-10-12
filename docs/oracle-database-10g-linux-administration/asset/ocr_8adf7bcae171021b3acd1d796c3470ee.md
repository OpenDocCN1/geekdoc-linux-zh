# Adding Datafiles to a Tablespace

It can be faster to add datafiles to a tablespace than to specify them at tablespace creation since adding datafiles can be done in parallel. Datafile creation at tablespace creation time is done serially, one at a time. For a large tablespace creation, this can save significant time.

# Adding Datafiles

It is often necessary to add more datafiles to a tablespace if you need more space or want to spread out I/Os among more disk drives. It is also faster to add datafiles to a tablespace than to create them at database creation time. The CREATE TABLESPACE command works serially, that is, it creates one datafile at a time. By adding datafiles, this operation can be parallelized; thus, multiple datafiles can be added to a tablespace simultaneously.

Datafiles are added by using the ALTER TABLESPACE command, as shown in this example.

```
ALTER TABLESPACE ts1
ADD DATAFILE '/u01/app/oracle/oradata/orac/ts01b.dbf' SIZE 10M;
```

This command will add an additional 10MB datafile to the tablespace named ts1.

# Altering Tablespace Properties

Other properties of the tablespace that can be changed via the ALTER TABLESPACE command are

+   1. Add or rename a datafile

+   2. Bring it offline or online

+   3. Coalesce the extents in a dictionary managed tablespace

+   4. Begin or end backup mode

+   5. Change from permanent to temporary or temporary to permanent

+   6. Change the storage clause, size, or put it into autoextent mode

As you can see, there are a number of options.

# Read-Only Tablespaces

As described earlier, it is possible to alter a tablespace to make it read-only. Read-only tablespaces are similar to read-write tablespaces with the restriction that no changes can be made to the schema objects residing on those tablespaces. When a tablespace is made read-only, the need to back up this tablespace is eliminated.