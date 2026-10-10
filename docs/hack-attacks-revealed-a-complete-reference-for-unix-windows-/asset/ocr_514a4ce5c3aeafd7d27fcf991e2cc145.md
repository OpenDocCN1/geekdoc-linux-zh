```
#include <stdio.h>
#include <string.h>

main()
{
  char data[50];
  char *p;

  strcpy(data,"RED,ORANGE,YELLOW,GREEN,BLUE,INDIGO,VIOLET");

  for(strtok(data,", "); p; p = strtok(NULL,", "))
  {
    puts(p);
  };
}
```

Initially, you call strtok() with the name of the string variable to be parsed, and a second string that contains the known delimiters. Strtok() then returns a pointer to the start of the first substring and replaces the first token with a zero delimiter. Subsequent calls to strtok() can be made in a loop, passing NULL as the string to be parsed; strtok() will return the subsequent substrings. Since strtok() can accept numerous delimiter characters in the second parameter string, you can use it as the basis of a simple word-counting program:

```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

void main(int argc, char *argv[ ])
{
  FILE *fp;
  char buffer[256];
  char *p;
  long count;

  if (argc != 2)
  {
    fputs("\nERROR: Usage is wordcnt <file>\n",stderr);
    exit(0);
  }

  /* Open file for reading */
  fp = fopen(argv[1],"r");

  /* Check the open was okay */
  if (!fp)
  {
    fputs("\nERROR: Cannot open source file\n",stderr);
    exit(0);
  }

  /* Initialize word count */
  count = 0;

  do
```