```
/* module_param(foo, int, 0000)
 * The first param is the parameter's name.
 * The second param is its data type.
 * The final argument is the permissions bits.
 * for exposing parameters in sysfs (if non-zero) at a later stage.
 */
module_param(my short, short, S_IRUSR | S_IWUSR | S_IRGRP | S_IWGRP);
MODULE_PARAM_DESC(my short, "A short integer");
module_param(my int, int, S_IRUSR | S_IWUSR | S_IRGRP | S_IROTH);
MODULE_PARAM_DESC(my int, "An integer");
module_param(my long, long, S_IRUSR);
MODULE_PARAM_DESC(my long, "A long integer");
module_param(my string, charp, 0000);
MODULE_PARAM_DESC(my string, "A character string");

/* module_param_array(name, type, num, perm);
 * The first param is the parameter's name.
 * The second param is the data type of the elements of the array.
 * The third argument is a pointer to the variable that will store the number
 * of elements of the array initialized by the user at module loading time.
 * The fourth argument is the permission bits.
 */
module_param_array(my int array, int, &arr_argc, 0000);
MODULE_PARAM_DESC(my int array, "An array of integers");

static int __init hello_5_init(void)
{
    int i;

    pr_info("Hello, world \n==============\n");
    pr_info("my short is a short integer: %dn", my short);
    pr_info("my int is an integer: %dn", my int);
    pr_info("my long is a long integer: %ldn", my long);
    pr_info("my string is a string: %sn", my string);

    for (i = 0; i < ARRAY_SIZE(my int array); i++)
        pr_info("my int array[%d] = %dn", i, my int array[i]);

    pr_info("got %d arguments for my int array.\n", arr_argc);
    return 0;
}

static void __exit hello_5_exit(void)
{
    pr_info("Goodbye, world \n");
}

module_init(hello_5_init);
module_exit(hello_5_exit);
```

It is recommended to experiment with the following code:

```
$ sudo insmod hello-5.ko mystring="bebop" myintarray=-1
$ sudo dmesg -t | tail -7
my short is a short integer: 1
```