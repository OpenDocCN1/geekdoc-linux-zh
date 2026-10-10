# DESCRIPTION

The tool reads problem directory DIR, asseles an micro report from the loaded problem data and sends the micro report to uReport server for updating statistics and fast analysis. The results of the analysis are stored in problem data in form of problems elents. *reporter-ureport* updates *reported_to*

# Configuration file

If not specified, *CONFFILE* defaults to /etc/libreport/plugins/ureport.conf. Configuration file lines should have *PARAM = VALUE* format. The paraters are:

+   * URL

Base sever HTTP(S) address.

+   * SSLVerify

Use no/false/off/0 to disable verification of server's SSL certificate. (default: yes)

+   * SSLCLientAuth

If this option is set, client-side SSL certificate is used to authenticate to the server so that it knows which machine it ca from. Assigning any value to this option changes the default value of IncludeAuthData to yes.

Possible values are:

+   * rhsn

Uses the system V3 entitelent certificate that is used for Red Hat subscription management.

+   * puppet

Uses the certificate that is used by the Puppet configuration managment tool.

+   * <cert_path>:<key_path>

Manually supply paths to certificate and the corresponding key in PEM format.

+   * HTTPAuth

Use the configured values to as HTTP Basic Authentication credentials. Assigning any value to this option changes the default value of IncludeAuthData to yes.

Possible values are

+   * rhts-credentials

Uses *Login=* and *Password=* values from /etc/libreport/plugins/rhtssupport.conf.