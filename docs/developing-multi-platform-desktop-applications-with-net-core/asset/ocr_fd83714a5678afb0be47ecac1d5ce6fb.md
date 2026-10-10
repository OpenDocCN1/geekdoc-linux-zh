+   2. The view used for the positioning of the widget and his docking, packing in the GTK terminology (with the tab “Packing”).

+   3. The view used for common properties of the current selected widget (with the tab “Common”).

+   4. The view for the management of the signal sent on different event associated to a widget (with the tab “Signals”).

These simple concepts are sufficient for the design of an efficient GUI for your application with Glade.

Note that, the mastering of Glade is not immediate and should require a learning curve, variable according to the developer.

# 8.5.4.3 Defining Signals/Handler within Glade

Once you have done the graphical design, Glade can be used for making the link between the interface and your backend program (the C# code).

GTK follow an architecture of type signal/handler (a classic). With this logic, Glade allow the developer to specify the type of signal sent by an event on a specific widget (within the right panel). This implementation is done directly from the Glade application by the specification of the appropriate method name call on a specific signal as described (figure 3).

You will notice some signal are marked “deprecated” in the Glade interface but you can use the deprecated signals too (as in the shoot screen).