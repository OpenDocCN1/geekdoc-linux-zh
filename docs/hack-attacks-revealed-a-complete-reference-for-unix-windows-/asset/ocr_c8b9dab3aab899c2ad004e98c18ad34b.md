```
```text
void OPENDATA(void);
int SEARCH(void);

void CLS()
{
int n;

for (n = 0; n < num_lines; n++)
puts(" ");
}

void FATAL(char *error)
{
printf("\nFATAL ERROR: %s", error);
exit(0);
}

void OPENDATA()
{
/* Check for existence of data file and if not create it */
/* otherwise open it for reading/writing at end of file */
handle = open("address.dat", O_RDWR | O_APPEND, S_IWRITE);

if (handle == -1)
{
handle = open("address.dat", O_RDWR | O_CREAT, S_IWRITE);
if (handle == -1)
FATAL("Unable to create data file");
}
}

void GETDATA()
{
/* Get address data from operator */

CLS();

printf("Name ");
gets(record.name);
printf("\nAddress ");
gets(record.address);
printf("\nTown ");
gets(record.town);
printf("\nCounty ");
gets(record.county);
printf("\nPost Code ");
gets(record.post);
printf("\nTelephone ");
gets(record.telephone);
}

void DISPPDATA()
```
```