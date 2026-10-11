```

	t{-f <key>}\
	t{-g <key>}\
	t{-l}"}\
	exit(EXIT_FAILURE);
}

```

The user program, `mcdbcli.c`, is suitable for use in shell scripts. It expects one of five options on the command line: `-a` to add a record, `-d` to delete a record, `-f` to find a record, `-g` to get a record, or `-l` to list all records. The `-a` option requires two arguments, a key and a value to add to the database. `-d`, `-f`, and `-g` require one argument, a key. The `-l` option does not require any arguments because it simply dumps all the records in the database.

A useful enhancement would be to remove the static buffer size limit for the record listing operation. As it is written, each pointer in the table of keys and records is limited to 1024 bytes. For convenience, the code in question is reproduced here:

```
/* Size each element */
for(i = 0; i < cnt; ++i) {
	if((keys[i] = malloc(BUFSZ)) == NULL) {
		puts("mcdbcli.c: malloc keys[i]");
		exit(EXIT_FAILURE);
	}
	if((values[i] = malloc(BUFSZ)) == NULL) {
		puts("mcdbcli.c: malloc values[i]");
		exit(EXIT_FAILURE);
	}
}
```

As it stands, this segment is acceptable because it is hard to imagine a musician's name or a CD title that will exceed `BUFSZ` bytes (which is `#defined` to be 1024 bytes). Nevertheless, the principle at stake is to avoid arbitrary limits such as this, no matter how reasonable they seem at the time.

To parse the command line, the program uses the POSIX `getopt` function, declared in `<getopt.h>` (you also must `#include <unistd.h>`), as follows:

```
int getopt(int argc, char *const argv[], const char *optstring);
```

`argc` and `argv` are the `argc` and `argv` parameters to `main`. `getopt` expects each option to be preceded by a dash (`-`). `optstring` contains a list of valid option characters. If a character in `optstring` is followed by a colon (`:`), it must be followed on the command line by an argument.