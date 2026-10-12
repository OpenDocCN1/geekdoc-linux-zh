```
```c
int     i, wordCount = 0;
bool    lookingForWord = true, alphabetic (const char  c);

for ( i = 0;  string[i] != '\0';  ++i )
if ( alphabetic(string[i]) )
{
        if ( lookingForWord )
        {
                ++wordCount;
                lookingForWord = false;
        }
}
else
        lookingForWord = true;

return wordCount;
}

int main (void)
{
        char  text[81];
int     totalWords = 0;
int     countWords (const char  string[]);
void    readLine (char  buffer[]);
bool    endOfText = false;

        printf ("Type in your text.\n");
        printf ("When you are done, press 'RETURN'.\n\n");

        while ( ! endOfText )
        {
                readLine (text);

                if ( text[0] == '\0' )
                        endOfText = true;
                else
                        totalWords += countWords (text);
        }

        printf ("\nThere are %i words in the above text.\n", totalWords);

        return 0;
}
```

```