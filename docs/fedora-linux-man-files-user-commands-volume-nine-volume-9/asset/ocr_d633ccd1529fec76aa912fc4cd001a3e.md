<user_na>∶<password>

Manually supply credentials.

# *ContactEmail*

Email address attached to a bthash on the server.

# *IncludeAuthData*

If this option is set to yes, uploaded uReport will contain auth object consisting from key value pairs made from CSV list stored in AuthDataItems option. Keys are file nas and values are bites of these files.

The default value is no, unless you set SSLClientAuth to so value. In that case, the default value is yes.

# *AuthDataItems*

CSV list of files included in the auth uReport object.

Paraters can be overriden via SuReport_PARAM environmt variables.