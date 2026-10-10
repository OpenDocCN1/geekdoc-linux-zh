# ■ Understanding the Global Catalog

THE BOTTOM LINE
Although the global catalog is not one of the five FSMO roles, the services it provides are of critical importance to the functionality of the Active Directory network. The global catalog holds a subset of forest-wide Active Directory objects and acts as a central repository by holding a complete copy of all objects from the host server's local domain along with a partial copy of all objects from other domains within the same forest, called **the partial attribute set (PAS)**. This partial copy of forest-wide data includes a subset of each object's attributes. The attributes included in this subset are necessarily to provide functionality such as logon, object searches, and universal group memberships.

# Understanding the Functions of the Global Catalog

By default, the first domain controller installed in the forest root domain is designated as a global catalog server. However, any or all domain controllers in a domain can be designated as global catalog servers. As an Active Directory administrator, you need to carefully weigh the benefits of designating additional domain controllers in your environment as global catalogs against the resulting performance implications.

XREF
For more information about Active Directory's need for SRV record support in DNS, refer to **Lesson 2**.

The global catalog has four main functions in an Active Directory environment:

+   * Facilitating searches for objects in the forest. When a user initiates a search for an object in Active Directory, the request is automatically sent to **TCP port 3268**, which is used by Active Directory to direct these requests to a global catalog server. One of the **SRV records** used by Active Directory refers to the global catalog, or _gc_ service, which listens on port 3268 to respond to these requests.
+   * Resolving User Principal Names (UPNs). UPNs allow users to log on to domains across the forest using a standardized naming format that matches the format used for email addresses, such as jsmith@lucernepublishing.com. When a local domain controller receives a request for logon via a UPN, it contacts a global catalog server to complete the logon process. For example, assume the user account for jsmith resides in the lucernepublishing.com domain, and jsmith is currently working from the tdko.lucernepublishing.com location. Because jsmith travels frequently between the various corporate locations, he uses the UPN, jsmith@lucernepublishing.com, to log on to his network account and his email account. Upon receiving a logon attempt from jsmith, a local domain controller searches for a global catalog server to resolve jsmith@lucernepublishing.com to a username. The global catalog server stores enough information about the user to permit or deny the logon request. For example, if a time restriction allows logons only during business hours and jsmith is attempting to log on after hours, the global catalog will have a copy of that information and, therefore, jsmith's logon request will be denied. Because of this need to allow user authentication across domains, Active Directory must be able to contact a global catalog (or have a mechanism to cache global catalog information as you will see shortly) to process any user logon, even in a single-domain environment.

TAKE NOTE
UPN logons are also possible between forests that have a cross-forest trust established.