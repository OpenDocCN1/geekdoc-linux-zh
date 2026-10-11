```
```
16 int emp_id_compare(const void *e1p, const void *e2p)
17 {
18     const struct employee *e1, *e2;
19
20     e1 = (const struct employee *) e1p;
21     e2 = (const struct employee *) e2p;
22
23     if (e1->emp_id < e2->emp_id)
24         return -1;
25     else if (e1->emp_id == e2->emp_id)
26         return 0;
27     else
28         return 1;
29 }
30
31 /* print_employee --- print an employee structure */
32
33 void print_employee(const struct employee *emp)
34 {
35     printf("%s %s\t%d\t%s", emp->lastname, emp->firstname,
36            emp->emp_id, ctime(&emp->start_date));
37 }
```
```

Lines 7–12 define the struct employee; it’s the same as before. Lines 16–29 serve as the comparison function, for both qsort() and bsearch(). It compares on employee ID number only. Lines 33–37 define print_employee(), which is a convenience function for printing the structure since this is done from multiple places.

```
```
39 /* main --- demonstrate sorting */
40
41 int main(int argc, char *argv)
42 {
43     #define NPRES 10
44     struct employee presidents[NPRES];
45     int i, npres;
46     char buf[BUFSIZ];
47     struct employee *the_pres;
48     struct employee key;
49     int id;
50     FILE *fp;
51
52     if (argc != 2) {
53         fprintf(stderr, "usage: %s datafile\n", argv[0]);
54         exit(1);
55     }
56
57     if ((fp = fopen(argv[1], "r")) == NULL) {
58         fprintf(stderr, "%s: %s: could not open: %s\n", argv[0],
59                 argv[1], strerror(errno));
60         exit(1);
61     }
62
```
```