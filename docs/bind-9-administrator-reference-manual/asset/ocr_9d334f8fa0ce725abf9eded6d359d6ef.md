);

and it had an identical key statement for rndc_key.

Running the rndc-confgen program will conveniently create a rndc.conf file for you, and also display the corresponding controls statement that you need to add to named.conf. Alternatively, you can run rndc-confgen -a to set up a rndc.key file and not modify named.conf at all.

# # 3.4.2. Signals

Certain UNIX signals cause the name server to take specific actions, as described in the following table. These signals can be sent using the kill command.

| | |
|---|---|
| SIGHUP | Causes the server to read named.conf and reload the database. |
| SIGTERM | Causes the server to clean up and exit. |
| SIGINT | Causes the server to clean up and exit. |