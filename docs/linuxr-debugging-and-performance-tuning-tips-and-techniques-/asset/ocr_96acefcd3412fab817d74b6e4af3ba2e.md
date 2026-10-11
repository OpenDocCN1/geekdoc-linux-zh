are zero). In such a case, the subtraction result would automatically be cast to `int`, throwing away the upper 32 bits and returning an incorrect value.

NOTE We could have stopped with the comparison on first names, in which case all employees with the same last and first names would be grouped, but *without any other ordering*.
This point is important: `qsort()` does not guarantee a stable sort. A *stable* sort is one in which, if two elements compare equal based on some key value(s), they will maintain their original ordering, relative to each other, in the final sorted array. For example, consider three employees with the same first and last names, with employee numbers 17, 42, and 81. Their order in the original array might have been 42, 81, and 17. (Meaning, employee 42 is at a lower index than employee 81, who, in turn, is at a lower index than employee 17.) After sorting, the order might be 81, 42, and 17. If this is an issue, then the comparison routine must take *all* important key values into consideration. (Ours does.)

Simply by using a different function, we can sort employees by seniority:

```
```
int emp_seniority_compare(const void *elp, const void *e2p)
{
	const struct employee *e1, *e2;
	double diff;

	e1 = (const struct employee *) elp;              Cast pointers to correct type
	e2 = (const struct employee *) e2p;

diff = difftime(e1->start_date, e2->start_date);   Compare times
	if (diff < 0)
		return -1;
	else if (diff > 0)
		return 1;
	else
		return 0;
}
```
```

For maximum portability we have used `difftime()`, which returns the difference in seconds between two `time_t` values. For this specific case, a cast such as—
`return (int) difftime(e1->start_date, e2->start_date);`