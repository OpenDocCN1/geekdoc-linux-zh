```
```c
sprintf(vbuf, "%.*s", 
        (int)value.size, (char *)value.data);
show(kbuf, vbuf);
break;
case KEY_F(6):    /* F6 - List all records */
if((cnt = count_recs()) == 0) {
    status("No records in database");
break;}
/* Size a table of pointers */
if((keys = malloc(sizeof(DBT *) * cnt)) == NULL
    status("Memory error");
if((values = malloc(sizeof(DBT *) * cnt)) == NULL
    status("Memory error");
/* Size each pointer in the table */
for(i = 0; i < cnt; ++i) {
    if((keys[i] = malloc(BUFSZ)) == NULL) {
        status("Memory error");
        break;}
    if((values[i] = malloc(BUFSZ)) == NULL) {
        status("Memory error");
        break;}
}
/* Get all of the records */
ret = list_recs(keys, values);
if(ret == 0) {
    status("Problem with database manager");
break;}
/* Show 'em on the screen */
for(i = 0; i < cnt; ++i) {
    sprintf(kbuf, "%s.*s",  (int)strlen(keys[i]), keys[i]);
    sprintf(vbuf, "%s.*s",  (int)strlen(values[i]), values[i]);
    list(kbuf, vbuf, i);
}
status("Last record displayed");
```
```