```
```text
        ok = 0;
if (*rec.county)
    if (strcmp(buffer.county,rec.county))
        ok = 0;
if (*rec.post)
    if (strcmp(buffer.post,rec.post))
        ok = 0;
if (*rec.telephone)
    if (strcmp(buffer.telephone,rec.telephone))
        ok = 0;
if (*rec.fax)
    if (strcmp(buffer.fax,rec.fax))
        ok = 0;
if (ok)
{
    blanks = total_lines;
    p = buffer.name;
    ok2 = 0;
    while(*p)

        {
        if (*p != 32)
        {
        ok2 = 1;
        break;
        }
        p++;
        }
    if (!ok2)
        blanks++;
    else
        fprintf(fp,"%s\n",buffer.name);
    p = buffer.company;
    ok2 = 0;
    while(*p)
    {
        if (*p != 32)
        {
        ok2 = 1;
        break;
        }
        p++;
        }
    if (!ok2)
        blanks++;
    else
        fprintf(fp,"%s\n",buffer.company);
    p = buffer.address;
    ok2 = 0;

    while(*p)

        {
        if (*p != 32)
```

```