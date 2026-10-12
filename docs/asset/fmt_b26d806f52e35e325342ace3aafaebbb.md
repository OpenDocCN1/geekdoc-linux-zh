
```
TRUST_AUTH_MECH 'EXTERNAL DIGEST-CRAM-MD5 LOGIN PLAIN'dnl

define('AUTH_MECHANISMS','EXTERNAL GSAPIT DIGEST-CRAM-MD5 LOGIN PLAIN')'dnl
```

这些行指定了身份验证机制。
接下来，取消 `sendmail.mc` 中以下行的注释，告诉 sendmail 您的证书所在位置：

```
define('CONFCACERT_PATH','/etc/pki/tls/certs')'dnl

def('CONFCACERT','/etc/pki/tls/certs/ca-bundle.crt')'dnl

def('CONFSERVER_CERT','/etc/pki/tls/certs/sendmail.pem')'dnl

def('CONFSERVER_KEY','/etc/pki/tls/certs/sendmail.pem')'dnl
```

加密连接通过两种方式之一建立：SSL（更简单）或 TLS。SSL 需要一个专用端口，并由客户端和服务器协商安全连接，如果连接未加密，则继续交易。TLS 允许客户端使用不安全的连接到服务器，并发出 `STARTTLS` 来协商安全连接。TLS 在与未加密连接相同的端口上运行。由于许多客户端仅支持 SSL，因此指示 sendmail 监听 SMTPS 是一个好主意。您需要在 `sendmail.mc` 中取消注释的最后一行指示 sendmail 监听 SMTPS（安全 SMTP）端口：

```
DAEMON_OPTIONS=('Port=smtps, Name=TLS, Msm=s')\1
```
