# my-small.cnf

This options file is recommended for computer systems that have less than 64MB of memory and are only used occasionally for MySQL. With this options file, MySQL won't be able to handle a lot of usage but it won't be a drag on the performance of your computer.

For the mysqld server, buffer sizes are set low - only 64K for the `sort_buffer` and 16K for the `key_buffer`. The `thread_stack` is only set to 64K and `net_buffer_length` is only 2K. The `table_cache` is set to 4.

# my-medium.cnf

As with the small options file, the my-medium.cnf file is intended for systems where MySQL is not the only important application running. This system also has a small amount of total memory available - between 32MB and 64MB - however more consistent MySQL use is expected.

The `key_buffer` size is set to 16M in this file, while the `sort_buffer` value is raised to 512K for the mysqld server. The `table_cache` is set to 64 (allowing more simultaneous threads to be active). The `net_buffer_length` is raised to 8K.

# my-large.cnf

The my-large.cnf sample file is intended for computers that are dedicated primarily to MySQL service. It assumes about 512M of available memory.

Server buffers allow more active threads and better sorting performance. Half of the system's assumed 512M of memory is assigned to the `key_buffer` variable (256M). The `sort_buffer` size is raised to 1M. The `table_cache` allows more simultaneous users (up to 256 active threads).

# my-huge.cnf

As with the my-large.cnf file, the my-huge.cnf file expects the computer to be used primarily for MySQL. However, the system for which it is intended offers much more total memory (between 1G and 2G of memory).

Sort buffer size (`sort_buffer`) is raised to 2M while the `key_buffer` is set to consume 384M of memory. The `table_cache` size is doubled to allow up to 512 active threads.

# Starting the MySQL Server

For Red Hat Linux, the MySQL server is off by default. To turn it on, however, is fairly simple. The /etc/init.d/mysqld start-up script is delivered with the mysql-server package. To start the server, you can either run the mysqld start-up script manually or set it to start each time your system boots.