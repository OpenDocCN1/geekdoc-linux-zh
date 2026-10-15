
```c
void process_A(void) {

    acquire_lock(&resource_1);

    while (try_lock(&resource_2) == FAIL) {

        release_lock(&resource_1);

        wait_fixed_time();

        acquire_lock(&resource_1);

    }

    use_both_resources();

    release_lock(&resource_2);

    release_lock(&resource_1);

}
```

```c
void process_B(void) {

    acquire_lock(&resource_2);

    while (try_lock(&resource_1) == FAIL) {

        release_lock(&resource_2);

        wait_fixed_time();

        acquire_lock(&resource_2);

    }

    use_both_resources();

    release_lock(&resource_1);

    release_lock(&resource_2);

}
```
