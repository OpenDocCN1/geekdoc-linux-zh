Most people should be looking to get more than 95% served from RAM, although the primary exception is if you update or delete rows very often—MySQL can’t cache what keeps changing. If your site is largely read only, this should be around 98%. Lower figures mean you might need to bump up the size of your key buffer.

If you are seeing problems, the next step is to check how much of your current key buffer is being used. Use the SHOW VARIABLES command and look up the value of the key_buffer_size variable. It is probably something like 8388600, which is eight million bytes, or 8MB. Now, use the SHOW STATUS command and look up the value of Key_blocks_used.

You can now determine how much of your key buffer is being used by multiplying Key_blocks_used by 1024, dividing by key_buffer_size and multiplying by 100. For example, if Key_blocks_used is 8000, you multiply that by 1024 to get 8192000; then you divide that by your key_buffer_size (8388600) to get 0.97656, and finally multiply that by 100 to get 97.656. Thus, almost 98% of your key buffer is being used.

Now, onto the important part: You have ascertained that you are reading lots of keys from disk, and you also now know that the reason for reading from disk is almost certainly because you do not have enough RAM allocated to the key buffer. A general rule of thumb is to allocate as much RAM to the key buffer as you can, up to a maximum of 25% of system RAM—128MB on a 512MB system is about the ideal for systems that read heavily from keys. Beyond that, you will actually see drastic performance decreases because the system has to use virtual memory for the key buffer.

Open /etc/my.cnf in your text editor, and look for the line that contains key_buffer_size. If you do not have one, you need to create a new one—it should be under the line [mysqld]. When you set the new value, do not just pick some arbitrarily high number. Try doubling what is there right now (or try 16MB if there’s no line already); then see how it goes. To set 16MB as the key buffer size, you would need line like this:

```
[mysqld]
set-variable = key_buffer_size=16M
datadir=/var/lib/mysql
```

Restart your MySQL server with service mysqld restart, and then go back into MySQL and run SHOW VARIABLES again to see the key_buffer_size. It should be 16773120 if you have set it to 16M. Now, because MySQL just got reset, all its values for key hits and the like will also have been reset. You need to let it run for a while so you can assess how much has changed. If you have a test system you can run, this is the time to run it.

After your database has been accessed with normal usage for a short while (if you get frequent accesses, this might be only a few minutes), recalculate how much of the key buffer is being used. If you get another high score, double the size again, restart, and retest. You should keep repeating this until you see your key buffer usage is below 50% or you find you don’t have enough RAM to increase the buffer further—remember that you should never allocate more than 25% of system RAM to the key buffer.