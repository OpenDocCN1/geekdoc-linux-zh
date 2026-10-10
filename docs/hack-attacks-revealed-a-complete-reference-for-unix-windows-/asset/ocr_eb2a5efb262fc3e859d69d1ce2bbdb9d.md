```
{
/* Read a line of data from the file */
fgets(buffer,255,fp);

/* check for an error in the read or EOF */
if (ferror(fp) || feof(fp))
continue;

/* count words in received line */
/* Words are defined as separated by the characters */
/* \t(tab) \n(newline) , ; : . ! ? ( ) - and [space] */
p = strtok(buffer,"\t\n,;:!.?() - ");
while(p)
{
count++;
p = strtok (NULL,"\t\n,;:!.?() - ");
}
while(!ferror(fp) && !feof(fp));

/* Finished reading. Was it due to an error? */
if (ferror(fp))
{
fputs("\nERROR: Reading source file\n",stderr);
fclose(fp);
exit(0);
}

/* Reading finished due to EOF, quite valid so print count */
printf("\nFile %s contains %ld words\n",argv[1],count);
fclose(fp);
}
```

# Converting Numbers To and From Strings

All C compilers provide a facility for converting numbers to strings such as sprintf( ) . However, sprintf( ) is a multipurpose function, meaning that it is large and slow. The function ITOS( ) can be used instead, as it accepts two parameters, the first being a signed integer and the second being a pointer to a character string. It then copies the integer into the memory pointed to by the character pointer. As with sprintf( ) , ITOS( ) does not check that the target string is long enough to accept the result of the conversion. An example function for copying a signed integer into a string would be:

```
void ITOS(long x, char *ptr)
{
/* Convert a signed decimal integer to a string */

long pt[9] = { 100000000, 10000000, 1000000, 100000, 10000, 1000
, 100, 10, 1 } ;
int n;

/* Check sign */
if (x < 0)
{
```