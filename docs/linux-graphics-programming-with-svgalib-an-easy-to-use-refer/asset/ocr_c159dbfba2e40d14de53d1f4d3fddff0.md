```
/* Forward declarations */
point *normalize(/* point *p */);
point *midpoint(/* point *a, point *b */);
void print_object(/* object *obj, int level */);
void print_triangle(/* triangle *t */);
void pphigs_header(/* int * */);
void pphigs_trailer();

extern char *malloc(/* unsigned */);

int main(int ac, char *av[])
{
    object *old,
    *new;
    int ccwflag = 0, /* Reverse vertex order if true */
        i,
        level, /* Current subdivision level */
        maxlevel = 1; /* Maximum subdivision level */

    /* Parse arguments */
    for (i = 1; i < ac; i++)
    {
        if (!strncmp(av[i], "-p"))
            PPHIGSFlag = 1;
        else if (!strncmp(av[i], "-c"))
            ccwflag = 1;
        else if ((maxlevel = atoi(av[i])) < 1)
        {
            fprintf(stderr, "%s: # of levels must be >-1\n", av[0]);
            exit(1);
        }
    }

    if (ccwflag)
    {
        /* Reverse order of points in each triangle */
        for (i = 0; i < oct.npoly; i++)
        {
            point tmp;

            tmp = oct.poly[i].pt[0];
            oct.poly[i].pt[0] = oct.poly[i].pt[2];
            oct.poly[i].pt[2] = tmp;
        }
    }

    old = &oct;
```