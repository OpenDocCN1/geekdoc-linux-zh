```
int i, j;
int temp;
int size;
int nums_to_compute;
thread_data *t_data = (thread_data*) data;

size = t_data->size;
nums_to_compute = nums_per_thread;

for ( i = 0; i < nums_to_compute; i++ ) {
    pthread_mutex_lock (&update_mutex);  /* lock mutex */
    temp = t_data->count;
    t_data->count = temp + 1;
    pthread_mutex_unlock (&update_mutex); /* unlock mutex */

    /* updating the array can be done outside of the CS since temp is
       a local variable to the thread. */
    t_data->roots[temp] = sqrt(temp);

    /* idle loop */
    for ( j = 0; j < 1000; j++ )
        ;
}
 pthread_exit( NULL );
}

/** compute_roots()
 * computes the square roots of the first num_threads*roots_per_thread many
 * integers. It hides the fact that it uses multiple threads to do this.
 */
void compute_roots( double sqrts[], int size, int num_threads )
{
    pthread_t threads[num_threads];
    int t;
    int retval;
    static thread_data t_data;

    t_data.count = 0;
    t_data.size = size;
    t_data.nums_per_thread = size / num_threads;
    t_data.roots = &sqrts[0];

    /* Initialize the mutex */
    pthread_mutex_init(&update_mutex, NULL);

    /* Initialize task_data for each thread and then create the thread */
    for ( t = 0 ; t < num_threads; t++ ) {
        retval = pthread_create(&threads[t], NULL, calc_square_roots,
                                (void *) &t_data);
        if ( retval )
            handle_error( retval, "pthread_create");
    }

    /* Join all threads and then print sum */
```