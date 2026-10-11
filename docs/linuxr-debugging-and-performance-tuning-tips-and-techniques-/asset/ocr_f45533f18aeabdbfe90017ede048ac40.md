longjmp() makes the jump. The first parameter is a jmp_buf that must have been initialized by setjmp(). The second is an integer nonzero value that setjmp() returns in the original environment. This is so that code such as that just shown can distinguish between setting the environment and arriving by way of a nonlocal jump.

The C standard states that even if longjmp() is called with a second argument of 0, setjmp() still returns nonzero. In such a case, it instead returns 1.

The ability to pass an integer value and have that come back from the return of setjmp() is useful; it lets user-level code distinguish the reason for the jump. For instance, gawk uses this capability to handle the break and continue statements inside loops. (The awk language is deliberately similar to C in its syntax for loops, with while, do-while, and for loops, and break and continue.) The use of setjmp() looks like this (from eval.c in the gawk 3.1.3 distribution):

```
```
507   case Node_K_while:
508       PUSH_BINDING(loop_tag_stack, loop_tag, loop_tag_valid);
509
510       stable_tree = tree;
511       while (eval_condition(stable_tree->lnode)) {
512           INCREMENT(stable_tree->exec_count);
513           switch (setjmp(loop_tag)) {
514               case 0: /* normal non-jump */
515                   (void) interpret(stable_tree->rnode);
516                   break;
517
518               case TAG_CONTINUE: /* continue statement */
519                   break;
520
521               case TAG_BREAK: /* break statement */
522                   RESTORE_BINDING(loop_tag_stack, loop_tag, loop_tag_valid);
523                   return 1;
524               default:
525                   cant_happen();
526               }
527           }
528       RESTORE_BINDING(loop_tag_stack, loop_tag, loop_tag_valid);
529       break;
```
```

This code fragment represents a while loop. Line 508 manages nested loops by means of a stack of saved jmp_buf variables. Lines 511–524 run the while loop (using a C while loop!). Line 511 tests the loop’s condition. If it’s true, line 513 does a switch on the setjmp() return value. If it’s 0 (lines 514–516), then line 515 runs the statement’s body. However, when setjmp() returns either TAG_BREAK or TAG_CONTINUE,