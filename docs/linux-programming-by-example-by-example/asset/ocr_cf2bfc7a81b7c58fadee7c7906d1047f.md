```
#include <string.h>	/* For 'memcpy' in glibc 2.1.1 */
#include "mcddb.h"	/* Database management */

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

	op = getopt(argc, argv, "a:d:f:g:1");

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
			perror("mcddcli.c: add_rec");
```