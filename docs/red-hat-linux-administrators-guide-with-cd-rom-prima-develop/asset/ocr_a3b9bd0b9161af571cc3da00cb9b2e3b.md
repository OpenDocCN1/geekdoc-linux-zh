Once you click the Activate button, the Network Configurator script will dial in to your Internet provider and begin executing the script you entered previously. With many of the PPP dial-in scripts provided, you will see a Debug button somewhere on the screen. This will assist in tracking down any errors you may encounter when attempting to dial into another provider.

# # Enabling a Dial-Up Connection under linuxconf

Setting up a similar connection under the linuxconf program can be just as simple and will also dial up and connect to the ISP. As shown in Figure 16.8, linuxconf’s routine is very similar to that of netcfg. The same windows are present along with the same fields. Here also you may activate the connection and edit the variables.

In both the netcfg and linuxconf windows, you can configure your machine so that it will activate the connection upon bootup. This allows you to connect immediately to the ISP as your machine comes on. Depending upon the fair use procedures defined by your ISP, you can remain online for as long as the ISP allows.

Under the very latest release of Red Hat Linux, the PPP/SLIP configuration interface is not available. It is recommended that users wishing to create a dial-up connection to an Internet Service Provider use the Red Hat PPP Dialer,

![](bbox=[0.05, 0.62, 0.71, 0.95])

# FIGURE 16.8
Configuring the entries under linuxconf for establishing a PPP connection.