# Build and Try it

Create the necessary make targets for the web thermostat, and try it out. Run it under the debugger on your workstation so you can watch what happens as a web browser accesses it. You must be running as root in order to bind to the HTTP port, 80.

In your favorite web browser enter:

http://127.0.0.1

into the destination window. You should see something like Fig. 10.4 once the file *index.html* is fully processed.

![](bbox=[0.11, 0.32, 0.86, 0.65])

Web thermostat.

When running the web thermostat on the target board, enter the IP address of your BBB into your web browser.

Once you have that running on both the workstation and target, here is an “extra credit” assignment. There are three small GIF files in the *network/* directory that are circles—one red, one green, and one open. These can be used to represent the states of the cooler and alarm. So try adding a couple of `<DATA>` tags that will put out the appropriate circle image based on the cooler and alarm states.