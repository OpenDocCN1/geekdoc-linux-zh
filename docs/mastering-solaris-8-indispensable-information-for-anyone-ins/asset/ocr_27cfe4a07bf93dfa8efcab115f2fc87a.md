limiting access to a printer, you will find that using the `1padmin` command is helpful and exceeds what you can currently do in the Print Manager.

Here is a list of some of the many options that the `1padmin` command takes:

+   - **-A option**  The -A (alert) option takes the form -A <alert-type> [-W minutes] and sets an alert action for a printer fault. You can specify a mail or console message (on the administrator's console) or use the quiet keyword to suppress error messages. You can also use `showFault` to specify a particular fault handling procedure or none to have no alerts generated. A shell command is one option for an alert action.

The LP print service sends alerts to the user as e-mails that specify a print request when it doesn't run correctly. Many problems, particularly print system problems, generate alerts that are sent to the administrator or superuser, typically appearing in a console window. A superuser can alter the nature of the alerts so that messages are sent either by e-mail or to a program that they specify. Alert messages can also be suppressed.

+   - **-c option**  The -c <classname> option specifies that the printer belongs to a particular class. If the class doesn't exist, the LP print system creates it.

+   - **-d option**  The -d <comment> option is used as a text description of the printer when a user requests information about that printer.

+   - **-e option**  The -e <printername> option copies the interface program used by an existing printer so it can be used with the printer you are adding.

+   - **-i option**  The -i <interface> option specifies the interface program used by the printer. Use the -e option when you are copying or cloning an already existing interface.

+   - **-m option**  The -m <model> selects a model interface program. When you select a model program, the -e and -i options do not apply.

+   - **-s option**  The -s <systemname> <printername> option can create a remote printer using a printer server that you specify with the <systemname> argument. The <printername> is the name of the remote printer that you use to identify the printer on your computer. That printer name does not have to match the remote printer name.

+   - **-x option**  The -x <printername> option removes a printer from the LP printing system. For example, `1padmin -xflash` would remove the printer named flash.