do_entry is used in one of two ways: If the stat_only argument is true or if the current entry isn’t a directory, it increments the global counters and then calls the callback function in SHOW_INFO mode. This is done when the -d argument is specified, when a nondirectory is specified on the aups command line, or during Pass 1 of a directory listing. Otherwise, for a directory, it calls the function do_dir that contains the readdir loops to process a directory’s entries:

```
static bool do_dir(struct traverse_info *p)
{
DIR *sp = NULL;
struct dirent *dp;
int dirfd = -1;
bool result = false;

ec_neg1( dirfd = open(".", O_RDONLY) )
if ( (sp = opendir(p->ti_name)) == NULL || chdir(p->ti_name) == -1) {
if (errno == EACCES) {
fprintf(stderr, "%s: Permission denied.\n", p->ti_name);
result = true;
EC_CLEANUP
}
EC_FAIL
}
if (p->ti_recursive)
ec_false( p->ti_fcn)(p, SHOW_PATH )
while (errno = 0, (dp = readdir(sp)) != NULL) {
if ( strcmp(dp->d_name, ".") == 0 ||
strcmp(dp->d_name, "..") == 0 )
continue;
p->ti_name = dp->d_name;
ec_false( do_entry(p, true) )
}
if (errno != 0)
syserr_print("Reading directory (Pass 1)");
if (p->ti_recursive) {
rewinddir(sp);
while (errno = 0, (dp = readdir(sp)) != NULL) {
if ( strcmp(dp->d_name, ".") == 0 ||
strcmp(dp->d_name, "..") == 0 )
continue;
p->ti_name = dp->d_name;
ec_false( do_entry(p, false) )
}
if (errno != 0)
syserr_print("Reading directory (Pass 2)");
}
result = true;
EC_CLEANUP
}
```