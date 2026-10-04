# XSQL Style Sheets

Earlier versions of the XSQL parser were vulnerable to arbitrary XML execution attacks. By specifying a style sheet that existed on another site, the Web server would connect to the remote server, download the XML, and execute whatever it contained. This problem was discovered by Georgi Guninski.

XML is actually a data format, which may be somewhat confusing. What actually occurs is SQL commands can be sent as XML data, and this XML will then be read and executed as XSQL.

# SOAP Application Deployment

The Simple Object Access Protocol (SOAP) is a simple and lightweight XML-based protocol designed to exchange structured and typed information on the Web. A typical install of Oracle 9iAS version 1.0.2.2 will install the Oracle SOAP components and allow anonymous users to deploy SOAP applications. Deploying SOAP applications should be restricted to administrators only. To determine if your Application Server is manageable, request the following:

```
http://oracleserver/soap/servlet/soaprouter
```

If the SOAP application soaprouter is present, the server has not been properly secured. This is done by adding the following element underneath the serviceManager element in the soap config file $ORACLE_HOME/soap/webapps/soap/WEB-INF/config/soapConfig.xml

```
<option name="autoDeploy" value="false" />
```

This deploys the urn:soap-service-manager and urn:soap-provider-manager services. The default configuration has the autoDeploy attribute set to true. For more information, see http://technet.oracle.com/deploy/security/pdf/ias_soap_alert.pdf.

# SOAP Configuration File

The soapConfig.xml file should be protected. It is not protected by default. It can be accessed directly or by using the XSQLServlet:

+   - http://oracleserver/soapdocs/webapps/soap/WEB-INF/config/soapConfig.xml
- http://oracleserver/servlet/oracle.xml.xql.XSQLServlet/soapdocs/webapps/WEB-INF/config/soapConfig.xml