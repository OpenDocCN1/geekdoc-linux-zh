# 6.2.8. key Statement Definition and Usage

The key statement defines a shared secret key for use with TSIG, see Section 4.4.

The key statement can occur at the top level of the configuration file or inside a view statement. Keys defined in top-level keys can be used in all views. Keys intended for use in a controls statement (see Section 6.2.4) must be defined at the top level.

The key_id, also known as the key name, is a domain name uniquely identifying the key. It can be used in a "server" statement to cause requests to server to be signed with this key, or in address match lists to verify that incoming requests have been signed with a key this name, algorithm, and secret.

The algorithm_id is a string that specifies a security/authentication algorithm. The only algorithm currently supported by TSIG authentication is hmac-md5. The secret_string is the secret used by the algorithm, and is treated as a base-64 encoded string.

# 6.2.9. logging Statement Grammar

```
logging {
  channel channel_name {
    file path name
    [ versions ( number | unlimited ) ]
    [ size size spec ]
    syslog syslog_facility
    stderr
    null);
    [ severity (critical | error | warning | notice | 
      info | debug [ level ] | dynamic ); ]
    [ print-category yes or no; ]
    [ print-severity yes or no; ]
    [ print-time yes or no; ]
  }
  [ category category_name {
    channel_name ; [ ... ]
  };
}
```