
```c
/*
 * mccli.c - Command-line driver for music CD database. Suitable
 * for use in shell scripts.
 */
#include <stdlib.h>		/* For 'exit' */
#include <unistd.h>
#include <getopt.h>		/* For 'getopt' */
#include <string.h>		/* For 'memcpy' in glibc 2.1.1 */
#include "mcddb.h"		/* Database management */

#define BUFSZ 1024

void usage(void);

int main(int argc, char **argv)
{
	int ret, op, cnt, i;
	extern char *optarg;	/* From <getopt.h> */
	extern int optind;	/* From <getopt.h> */
	DBT value;
	char **keys, **values;

	if (argc < 2 || argc > 4) {
		usage();
	}

	op = getopt(argc, argv, "a:d:f:g:l");

	if(open_db(NULL) == 1) {	/* Open the database */
		puts("Error opening database");
	}

	switch(op) {
	case 'a':			/* Add a record */
	/* But don't add an empty record or a zero-length key */
	if (argc == 4 &&
	    (optarg != NULL) &&
	    (strlen(optarg) >= 1) &&
	    (argv[optind] != NULL)) {
		ret = add_rec(optarg, argv[optind]);
		if(ret == 1) {
			printf("Key '%s' exists\n", optarg);
			exit(EXIT_FAILURE);
		} else if (ret < 0) {
			perror("mcdcli.c: add_rec");
			exit(EXIT_FAILURE);
		}
		break;
	} else {
		usage();
	}
	case 'd':                  /* Delete a record */
		if(argc == 3) {
			if(optarg != NULL) {
				ret = del_rec(optarg);
				if(ret == -1) {
					printf("Key '%s' not found\n", optarg);
					exit(EXIT_FAILURE);
				} else if(ret < 0) {
					perror("mcdcli.c: del_rec");
					exit(EXIT_FAILURE);
				}
			}
			break;
		} else {
			usage();
		}
	case 'f':                  /* Find a record */
		if(argc == 3) {
			if(optarg != NULL) {
				memset(&value, 0, sizeof(DBT));
				ret = find_rec(optarg, &value);
				if(ret == 1) {
					printf("Key '%s' not found\n", optarg);
					exit(EXIT_FAILURE);
				} else if(ret < 0) {
					perror("mcdcli.c: find_rec");
					exit(EXIT_FAILURE);
				}
			}
			printf("%s:%.*s\n", optarg,
				   (int)value.size, (char *)value.data);
			break;
		}
```
