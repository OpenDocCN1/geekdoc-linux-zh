# 2 DATA AND MEMORY

# 2.1 SIMPLE DATA TYPES?

When we write programs we have to make decisions or assertions about the nature of the world as we declare and describe variables to represent the kinds of things we want to include in our information processing.

This process is deeply philosophical; we make **ontological** assertions that this or that thing exists and we make **epistemological** assertions when we select particular data types or collections of data types to use to describe the attributes of these things. Heavy stuff with a great responsibility and not to be lightly undertaken.

As a practical example we might declare something that looks like the beginnings of a database record for geography.

```
```c
/********************************************************************
 * C Programming in Linux (c) David Haskins 2008
 * chapter2_1.c
 * ******************************************************************/

#include <stdio.h>
#define STRINGSIZE 256

int main(int argc, char *argv[])
{
    char town[STRINGSIZE] = "Guildford";
    char county[STRINGSIZE] = "Surrey";
    char country[STRINGSIZE] = "Great Britain";
    int population = 66773;
    float latitude = 51.238599;
    float longitude = -0.566257;
    printf("Town name: %s  population:%d\n",town,population);
    printf("County: %s\n",county);
    printf("Country: %s\n",country);
    printf("Location latitude: %f longitude: %f\n",latitude,longitude);
    printf("char = %d byte int = %d bytes float = %d bytes\n",
    sizeof(char),sizeof(int),sizeof(float) );
    printf("memory used:%d bytes\n",
    ((STRINGSIZE * 3) * sizeof(char) + sizeof(int) + (2 * sizeof(float)));
    return 0;
}
```
```