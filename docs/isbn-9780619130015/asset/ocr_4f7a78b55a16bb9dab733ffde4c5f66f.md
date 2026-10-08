4 Save the file.

5 Create the file `decode.c`. Enter this code:

```
```c
#include <stdio.h>

void decode_file(FILE *, FILE *);

int main()
{
    FILE *in_file, *out_file;
    char infile_name[81], outfile_name[81], input;
    printf("Enter the name of the file to decode: ");
    scanf("%s", infile_name);
    if ((in_file = fopen(infile_name, "r")) == NULL)
    {
        printf("Error opening %s\n", infile_name);
        exit(0);
    }
    printf("Enter the output file name: ");
    scanf("%s", outfile_name);
    if ((out_file = fopen(outfile_name, "w")) == NULL)
    {
        printf("Error opening %s\n", outfile_name);
        exit(0);
    }
    decode_file(in_file, out_file);
    printf("The file has been decoded.\n");
    fclose(in_file);
    fclose(out_file);
}
```
```

6 Save the file.

7 Create the file `decode_file.c`. Enter this code:

```
```c
#include <stdio.h>

void decode_file(FILE *in_file, FILE *out_file)
{
    while (!feof(in_file))
    {
        char input;

        input = fgetc(in_file);
        input -= 10;
        fputc(input, out_file);
    }
}
```
```