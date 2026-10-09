+   2. Run the configuration script.  
a. Enter `twadmin --create-polfile --site-keyfile /etc/tripwire/site.key /etc/tripwire/twpol.txt` to create policy file and key file.  
b. Enter **site#1** as the site key password.  
c. If necessary, enter the site key password again.  
d. If necessary, enter the local key password again.  
e. If necessary, enter the site key password two times to sign the configuration and policy files.  
f. Observe that the policy file is created.  
g. Change the permissions of the `twcfg.txt` and `twpol.txt` files so that only you can read and modify the files.

+   3. Initialize the Tripwire database.  
a. Enter `tripwire --init` to start initializing the database.  
b. Enter **loc@11** as the local password.  
c. Enter `/usr/sbin/twprint -m => d --print-dbfile` to create the database.

![](bbox=[0.62, 0.59, 0.97, 0.65])