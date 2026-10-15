+   9. Accept the default settings by selecting Next.
+   The Adding User dialog appears.

+   10. Accept the default settings by selecting Next.
+   The Miscellaneous Settings dialog appears.

+   11. Accept the default settings and configure the system for the new settings by selecting Finish.

+   12. To test the change, you must first activate the new configuration by rebooting the system or by entering (as root) init q (reload the /etc/inittab file) in a terminal window.
+   a. From the terminal window, su - to root (password novell).
+   b. Reload the file /etc/inittab by entering init q.

+   13. Verify that the Ctrl+Alt+Del setting has changed by entering grep ctrlaltdel /etc/inittab.
+   Notice that the setting is now “shutdown -h” instead of what you noted in Step 2.

+   14. Test this setting by pressing Ctrl+Alt+F2; then press Ctrl+Alt+Del.
+   The system shuts down instead of restarting.

+   15. Turn on your computer and log in to the Gnome desktop as geeko.

+   16. (Optional) Use the YaST Security settings module to change the default for Ctrl+Alt+Del back to restart.

(End of Exercise)