# **Applying select(2) to a Server**

The preceding text has described the select(2) function in some detail. Now it's time to put the function to work in an example. The next modified example of the RPN calculating server will make use of the select(2) function for real events only. This limitation was imposed to keep the programming example relatively short and simple to understand. The limitations of this demonstration will be discussed in more detail later.

The RPN server required a few modifications to the engine module rpneng.c, which are reflected in the new source module rpneng2.c. Rather than re-list the entire module, only the minor changes are shown in the context diff of Listing 11.4.

![](bbox=[0.1, 0.4, 0.2, 0.46])

```
**Listing 11.4:** rpneng2.c—diff -c rpneng.c rpneng2.c

```diff
$ diff -c rpneng.c rpneng2.c
*** rpneng.c		Mon Sep 13 22:13:56 1999
--- rpneng2.c		Wed Sep 15 21:55:20 1999
***************
*** 18,25 ***
 * RPN Stack:
 */
 
#define MAX_STACK		32
! static mpz_t *stack[MAX_STACK];
! static int sp = 0;
 
/*
 * Allocate a new mpz_t value:
--- 18,25 ----
 * RPN Stack:
 */
#define MAX_STACK		32
! mpz_t **stack;
! int sp = 0;
 
/*
 * Allocate a new mpz_t value:
***************
*** 45,51 **
*/
 * Free an allocated mpz_t value:
*/
! static void
 rpn_free(mpz_t **v) {
  mpz_clear(**v);
  free(*v);
```

```