# Webmin Actions Log

The Webmin Actions Log page provides access to the Webmin log. You can configure this log for each module and individual users. This module does not configure the logs, but provides you with a means to search the logs for actions performed by particular logged users or actions performed in given logged modules. Configuration of Webmin logging capabilities is covered in the Webmin Configuration section.

With this module it is possible to search for actions by specific users, within specific modules, for a given range of dates, or any combination of those qualifications. For example, if you manage a number of junior system administrators and you'd like to find out if one of them has edited an Apache virtual server configuration in the past week, this module makes those kinds of questions easy to answer (assuming logging to that degree is enabled, of course).

# Webmin Configuration

The Webmin Configuration module (Figure 3-1) allows you to configure most of the important aspects of Webmin itself, as well as install new modules, upgrade existing modules, and upgrade Webmin itself. It also provides a means to change the port and address where the Webmin miniserv.pl web server listens for connections, select different languages, enable or disable SSL encryption, and configure the Webmin built-in logging features.

![](bbox=[0.25, 0.57, 0.65, 0.83])

Figure 3-1: Webmin Configuration