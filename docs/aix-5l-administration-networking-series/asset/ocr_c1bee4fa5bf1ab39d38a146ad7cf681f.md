# # Internet and Documentation Services

Before you can use the DocSearch (Documentation Search Service), Netscape, or a search server, you must configure the access mechanisms (see Figure 8-8). Using the SMIIT FastPath `smit_web_configure` is the quickest way to set everything up. Normally, you can take the defaults except for the Search/Web Server. If you press F4, or ESC-4, you can see the list of installed products. Read your documentation for setting up these services and read Chapter 2 for details on setting up DocSearch. There is also an entry for the Web-Based System Manager (WebSM).

```
# smit_web_configure
```

# # Change the System User Interface

You have at least three options for a user interface, depending on the software installed on the server. I have the Common Desktop Environment installed, as well as all of the Linux desktops (KDE and GNome). You can use the SMIIT FastPath `smit dtconfig` to select between ASCII, CDE, and CDE with ASCII during boot.

![](bbox=[0.13, 0.48, 0.77, 0.84])

**Figure 8-8.** Internet And Documentation Services SMIIT panel