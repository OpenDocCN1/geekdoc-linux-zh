+   - Run client installation UI on `server`

Select: `Options -> Server Configurations... -> Session Options`

+   - Verify that only these options are set:
+       - `Confirm new clients`
+       - `Show the welcome screen for the install server`
+       - Ensure that the option `Hall the client after installation` is not selected.

![](bbox=[0.09, 0.3, 0.16, 0.41])

Once the Ignite-UX server is installed and configured to install HP-UX OEs and vPars, proceed to use `vparsboot` to install all remaining vPars as needed.

More information on Ignite-UX is available in the `Ignite-UX Administration Guide`.

As I mentioned at the beginning of this chapter, you'll probably have more instances of HP-UX 11i to manage when you use vPars. Installing these vPars from an Ignite-UX server will save you a lot of time and ensure that you have a consistent base of software for your installation.