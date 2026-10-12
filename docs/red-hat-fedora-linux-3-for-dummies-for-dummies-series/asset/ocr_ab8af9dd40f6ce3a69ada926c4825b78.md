# Chapter 8
# Only You Can Prevent Bad Firewalls

+   **In This Chapter**
+   
+   *   Introducing computer security
+   *   Using the Netfilter/iptables firewall system
+   *   Designing and viewing your filtering rules
+   *   Automatically starting your firewall
+   *   Automatically updating your computer software

After connecting to the Internet, you have to protect yourself from the bad guys. The bad guys wear black hats, just like in the movies (as opposed to red fedoras, which are a bit odd but good). You may also have heard them called hackers, crackers, black hats, and so on. Whatever their names and whatever their intentions, the Internet is getting more dangerous every day, so you have to take precautions.

No silver bullet exists when it comes to protecting yourself from computer mischief. You should not rely on any single method, or system, against hackers. The best defense is to create multiple lines of defense that overlap and provide extra protection. That's called defense-in-depth.

The first layer in your defensive shield is your firewall. A *firewall* is a device that enables you to use the Internet (or other network that's connected to it) while blocking the Internet from using you. Firewalls are one-way gates that allow your outgoing network connections while blocking incoming connections.

This chapter describes (not surprisingly) how to build a firewall. First, in case you doubt that you truly need a firewall, we explain why having