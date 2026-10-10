```
{
    int result;

    do
    {
        /* Read rec into memory */
        result = read(handle,&rec,reclsize);
        if (result > 0)
        {
            /* Scan rec for matching data */
            if (strstr(strupr(rec.name),text) != NULL)

                return(1);
            if (strstr(strupr(rec.company),text) != NULL)
                return(1);
            if (strstr(strupr(rec.address),text) != NULL)
                return(1);
            if (strstr(strupr(rec.area),text) != NULL)
                return(1);
            if (strstr(strupr(rec.town),text) != NULL)
                return(1);
            if (strstr(strupr(rec.county),text) != NULL)
                return(1);
            if (strstr(strupr(rec.post),text) != NULL)
                return(1);
            if (strstr(strupr(rec.telephone),text) != NULL)
                return(1);
            if (strstr(strupr(rec.fax),text) != NULL)
                return(1);
        }
    } while(result > 0);
    return(0);
}

void SEARCH()
{
    int result;

    gotoxy(left,21);
    textcolor(WHITE);
    textbackground(RED);
    cprintf("Enter data to search for ");
    strcpy(stext,"");
    INPUT(stext,30);
    if (*stext == 0)
    {
        gotoxy(left,21);
        cprintf("%70c",32);
        return;
    }
    gotoxy(left,21);
    textcolor(WHITE);
    textbackground(RED);

```

327