# Summary

The majority of security concerns with Terminal Server are not a result of a poor product, but a product that is implemented poorly. Terminal Server is a catalyst for low- and medium-severity vulnerabilities, offering them a change to reach the big time. For example, a simple low- to medium-severity vulnerability such as a guessable user account/password combination can result in remote command execution if that user has Terminal Server logon rights.

If you are new to the Terminal Server world, I recommend that you start using it as a remote administration tool only. Windows XP and Windows Server 2003 offer this in need to enable it. Thanks to their intuitive grouping of things like users with access to Terminal Services, these services are now very easy to manage. If you require application sharing on your internal network via Terminal Services, be ready for a steep road to the pinnacle of security. By allowing potential enemy access to your server, you have dramatically increased your risk of compromise. If you must travel this road, I recommend that you use Windows Server 2003 because it offers the most secure solution for multiuser scenarios.

Whichever usage of Terminal Services you select, don't forget the fundamentals of security, such as principle of least privilege, defense in depth, and patch management. Terminal Server is an enabling technology. If left on your network insecurely, this door will swing both ways, allowing access to defenders as well as attackers.

# Links to Sites

+   - http://msdn.microsoft.com/library/en-us/termserv/terminal_services_start_page.asp Microsoft Terminal Terminal Services Server SDK page.

+   - http://msdn.microsoft.com/library/en-us/termserv/terminal_services_api_functions.asp Microsoft's list of API's for Terminal Server.

+   - www.securityfocus.com Great all-around site for security information. Use the search feature to find useful information that is not easily located.