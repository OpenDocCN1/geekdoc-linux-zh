
/* Check to see if the memory allocation succeeded */
if (x == NULL)
{
   printf("\nUnable to allocate a 1000 element integer table");
   exit(0);
}

/* Assign values to each table element */
for(n = 0; n < 1000; n++)
{
   *x = n;
   x++;
}

/* Return x to the start of the table */
x -= 1000;

/* Display the values in the table */
for(n = 0; n < 1000; n++){ 
   printf("\nElement %d holds a value of %d",n,*x);
   x++;
}

/* Deallocate the block of memory now it's no longer required */
free(x);
}

Pointers are also used with character arrays, called strings. Since all C program strings are terminated by a zero byte, we can count the letters in a string using a pointer:

```c
#include <stdio.h>
#include <string.h>

main()
{
   char *p;
   char text[100];
   int len;

   /* Initialize variable 'text' with some writing */
   strcpy(text,"This is a string of data");

   /* Set variable p to the start of variable text */
   p = text;

   /* Initialize variable len to zero */
   len = 0;

   /* Count the characters in variable text */
   while(*p)
   {
      len++;
      p++;
   }

   /* Display the result */
   printf("\nThe string of data has %d characters in it",len);
}
```

To address 1MB of memory, a 20-bit number is composed of an *offset* and a 64KB *segment*. The IBM PC uses special registers called *segment registers* to record the segments of addresses. This introduces the C language to three new keywords: *near, far, and huge*.

- *Near pointers* are 16 bits wide and access only data within the current segment.
- *Far pointers* are composed of an offset and a segment address, allowing them to access data anywhere in memory.
- *Huge pointers* are a variation of the far pointer and can be successfully incremented and decremented through the entire 1 MB range (since the compiler generates code to amend the offset).

It will come as no surprise that code using near pointers executes faster than code using far pointers, which in turn is faster than code using huge pointers. To give a literal address to a far pointer, C compilers provide a macro, **MK_FP()**, which has the prototype:

```c
void far *MK_FP(unsigned segment, unsigned offset);
```

## Structures

C provides the means to group variables under one name, thereby providing a convenient means of keeping related information together and forming a structured approach to data. The general form for a structure definition is:

```c
typedef struct
{
  variable_type variable_name;
  variable_type variable_name;
}
structure_name;
```

When accessing data files with a fixed record structure, the use of a structure variable becomes essential. The following example shows a record structure for a very simple name and address file. It declares a data structure called data, composed of six fields: *name, address, town, county, post,* and *telephone*:

```c
typedef struct
{
  char name[30];
  char address[30];
  char town[30];
  char county[30];
  char post[12];
  char telephone[15];
}
data;
```

The individual fields of the structure variable are accessed via the following general format:

```
structure_variable.field_name;
```

There is no limit to the number of fields that may comprise a structure, nor do the fields have to be of the same types; for example:

```c
typedef struct
{
    char name[30];
    int age;
    char *notes;
}
dp;
```

This example declares a structure, dp, that is composed of a character array field, an integer field, and a character pointer field. Structure variables may be passed as a parameter by passing the address of the variable as the parameter with the ampersand (&) operator. The following is an example program that makes use of a structure to provide basic access to the data in a simple name and address file:

```c
#include <stdio.h>
#include <stdlib.h>
#include <io.h>
#include <string.h>
#include <fcntl.h>
#include <sys/stat.h>

/* num_lines is the number of screen display lines */
#define num_lines  25

typedef struct
{
    char name[30];
    char address[30];
    char town[30];
    char county[30];
    char post[12];
    char telephone[15];
}
data;

data record;
int handle;

/* Function prototypes */

void ADD_REC(void);
void CLS(void);
void DISPDATA(void);
void FATAL(char *);
void GETDATA(void);
void MENU(void);
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

void DISPDATA()
{
/* Display address data */
char text[5];

CLS();

printf("Name %s",record.name);
printf("\nAddress %s",record.address);
printf("\nTown %s",record.town);
printf("\nCounty %s",record.county);
printf("\nPost Code %s",record.post);
printf("\nTelephone %s\n\n",record.telephone);

puts("Press RETURN to continue");
gets(text);
}

void ADD_REC()
{
/* Insert or append a new record to the data file */
int result;

result = write(handle,&record,sizeof(data));

if (result == -1)
FATAL("Unable to write to data file");
}

int SEARCH()
{
char text[100];
int result;

printf("Enter data to search for ");
gets(text);
if (*text == 0)
return(-1);

/* Locate start of file */
lseek(handle,0,SEEK_SET);

do
{
/* Read record into memory */
result = read(handle,&record,sizeof(data));
if (result > 0)
{
/* Scan record for matching data */
if (strstr(record.name,text) != NULL)
return(1);
if (strstr(record.address,text) != NULL)
return(1);
if (strstr(record.town,text) != NULL)
return(1);
if (strstr(record.county,text) != NULL)
return(1);
if (strstr(record.post,text) != NULL)
return(1);
if (strstr(record.telephone,text) != NULL)
return(1);
}
}
while(result > 0);
return(0);
}

void MENU()
{
 int option;
 char text[10];

do
{
 CLS();
puts("\n\t\t\tSelect Option");
puts("\n\n\t\t\t1 Add new record");
puts("\n\n\t\t\t2 Search for data");
puts("\n\n\t\t\t3 Exit");
puts("\n\n\n\n");
gets(text);
option = atoi(text);

 switch(option)
{
 case 1 : GETDATA();
/* Go to end of file to append new record */
 lseek(handle,0,SEEK_END);
 ADD_REC();
 break;

 case 2 : if (SEARCH())
 DISPDATA();
 else
 {
 puts("NOT FOUND!");
 puts("Press RETURN to continue");
 gets(text);
 }
 break;

 case 3 : break;
 }
 while(option != 3);
}

void main()
{
 CLS();
 OPENDATA();
 MENU();
}
```

## Bit Fields

C allows the inclusion of variables with a size of fewer than 8 bits in structures. These variables are known as *bit fields*, and may be any declared size from 1 bit upward. The general form for declaring a bit field is as follows:

```
type name : number_of_bits;
```

For example, to declare a set of status flags, each occupying 1 bit:

```c
typedef struct
{
    unsigned carry : 1;
    unsigned zero  : 1;
    unsigned over  : 1;
    unsigned parity : 1;
}
df;

df flags;
```

The variable *flags*, then occupies only 4 bits in memory, yet is composed of four variables that may be accessed like any other structure field.

## Unions

Another facility provided by C for the efficient use of available memory is the *union* structure, a collection of variables that all share the same memory storage address. As such, only one of the variables is accessible at a given time. The general form of a union definition is shown here:

```c
union name
{
    type variable_name;
    type variable_name;
    .
    .
    .
    type variable_name;
} ;
```

## Enumerations

An enumeration assigns ascending integer values to a list of symbols. An enumeration declaration takes the following form:

```
enum name { enumeration list } variable_list;
```

To define a symbol list of colors, you can use:
