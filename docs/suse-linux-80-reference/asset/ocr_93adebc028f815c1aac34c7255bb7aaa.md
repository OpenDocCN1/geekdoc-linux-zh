DOC_HOST=""

If a global documentation server should be used for the SuSE help system, enter the name of the server here, for example, "sun.cosmos.com".

DOC_SERVER="no"

On the documentation server, this variable must be set to yes so, depending on the settings in DOC_ALLOW, access will be granted to http-man and the index files for the HTTP server will be modified accordingly. They will point to the documentation server instead of http://localhost.

DOC_ALLOW="LOCAL"

List of hosts and domains as a pattern for /etc/hosts.allow, which should have access to the documentation server. This variable will only be read if DOC_SERVER is set to yes. A subdomain can also be listed here (e.g., with "*.cosmos.com").

# **language** — Settings for language and locale

DEFAULT_LANGUAGE="english"

This variable is set by YaST automatically if you change the language settings in the control center. This value is used as a fallback if RC_LANG is not set. The value is passed on through the file /usr/share/locale/locale.alias.

RC_LANG="en_US"

Sets variable LANG for locale. This is the default for local users, as long as no RC_LC_* variables are used. The respective sysconfig variables are: RC_LC_ALL (overwrites LC_* and LANG!), RC_LC_MESSAGES, RC_LC_CTYPE, RC_LC_MONETARY, RC_LC_NUMERIC, RC_LC_TIME, and RC_LC_COLLATE.

See Section *Local Adjustments — I18N/L10N* on page 292.

ROOT_USES_LANG="no"

Should locale settings be used for root?

# **mail** — Settings for e-mail.

FROM_HEADER=""

From: line defined for the whole system. If empty "", FQDN is used. See Section *Domain Name System* on page 330.

MAIL_CREATE_CONFIG="yes"

Set this to no if SuSEconfig should not generate the configuration files (e.g., you want to generate your /etc/sendmail.cf yourself). If you want to generate a sendmail configuration /etc/sendmail.cf from parameters given in /etc/sysconfig/sendmail, use yes.