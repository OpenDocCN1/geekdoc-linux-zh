# Using the DOMAIN File

At the conclusion of Chapter 5, “Understanding a Vendor’s Configuration,” the redhat.mc file was rewritten to take advantage of the structure inherent in the Sendmail m4 configuration directory. In 5.6, the large redhat.mc file was divided into three files: a macro control file named redhat811.mc, an OTYPE file named redhat7.0.m4, and a DOMAIN file named foobirds.m4. Traditionally, the macro control file selects components, the OTYPE file operates system-specific values, and the DOMAIN file holds all configuration options that are specific to your network or domain. In the first few sections of this chapter, we stick to the traditional use of these files by making changes to the foobirds.m4 file, which is shown in Listing 9.1.

+   9.1 A Sample DOMAIN File

```
 # ../../foobirds.m4
VERSIONID(`Settings for the foobirds.org domain`)\dnl
define(`CONFORWARD_PATH`,
  $/forward.Sw+;h$/forward+$h:/z$/forward.Sw:/z;
  forward`)\dnl
define(`CONFUSER_DB_SPEC`, `/etc/mail/userdb.db`)\dnl
FEATURE(`always_add_db`)\dnl
FEATURE(`access_db`)\dnl
FEATURE(`blacklist_recipients`)\dnl
FEATURE(`redirect`)\dnl
FEATURE(`use_cw_file`)\dnl
EXPOSED_USER(`root`)\dnl
[root] m4 ../m4.cf redhat811.mc > plain.cf
[root] cp ../domain/foobirds.m4 ../domain/old-foobirds.m4
```

All of the commands in this file are explained in Chapter 5, and for the most part these existing commands don't have anything to do with the topics covered in this chapter. We process redhat811.mc, which is the macro control file that creates to be the baseline sendmail.cf file against which we can compare our changes. At the end of Listing 9.1, the original DOMAIN file is copied to foobirds.m4. That provides a backup file in case we don't like the changes we make in the next few sections, and an original against which we can compare the changes. The originals will be an important part of the test that helps us determine the impact of each configuration command.