![](bbox=[0.3, 0.13, 0.7, 0.33])

**Figure 7.2** Linked list of records.

```
```	ec_neg1( pid = fork( ) )
if (pid == 0)
    process1( );
else { 
    process2( ); 
    ec_neg1( waitpid(pid, NULL, 0) ) 
}
exit(EXIT_SUCCESS);

EC_CLEANUP_BGN 
    exit(EXIT_FAILURE); 
EC_CLEANUP_END 
}
```
```

For data, process1 just counts backwards from 1000 after writing the header record:

```
```
#define DBNAME "termdb"

static void process1(void)
{
    int dbfd, data;
    struct rec r;

    ec_neg1( dbfd = open(DBNAME, O_CREAT | O_TRUNC | O_RDWR, PERM_FILE) )
    memest(&r, 0, sizeof(r));
    ec_false( writerec(dbfd, &r, 0) )
    for (data = 100; data >= 0; data--)
        ec_false( store(dbfd, data) )
    ec_neg1( close(dbfd) )
    exit(EXIT_SUCCESS);

EC_CLEANUP_BGN 
    exit(EXIT_FAILURE); 
```
```