to display all the records in the database (comparable to the −1 option of `mcdcli.c`). It tries to arrange the output in an attractive fashion on the screen. The `cnt` argument is key. When `cnt` is 0, no records have yet been displayed, so `list` first creates a header before displaying a record. Thereafter, `list` updates the working window, `workwin`, with the next record. A useful improvement in this function would be to enable scrolling in the working window if the total number of records to show exceeds the number of rows that `workwin` has.

The real meat of the interactive interface lives in `mcdui.c`, presented next.

```
/ * 
* mcdui.c - Ncurses-based driver for music CD database. 
*/
#include <stdlib.h> /* For 'exit' */
#include <unistd.h>
#include <getopt.h> /* For 'getopt' */
#include <string.h> /* For 'memcmp' in glibc 2.1.1 */
#include "mccdd.h" /* Database management */
#include "mcdsc.h" /* Screen handling */

#define BUFSZ 1024

void usage(void);

int main(int argc, char **argv)
{
 int ret, opt, fkey, cnt, i;
 extern char *optarg; /* From <getopt.h> */
 char kbuf[BUFSZ], vbuf[BUFSZ];
 char **keys, **values;
 DBT value;

 /* Parse the command line */
 switch(argc) {
 case 3: /* Use the specified database */
 opt = getopt(argc, argv, "f:");
 if(opt == 'f') {
 if(optarg == NULL) {
 usage();
 } else {
```