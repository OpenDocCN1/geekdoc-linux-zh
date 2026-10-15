If you name your zone data files after the zones and maintain the names of the original key files, the command reduces to

```
dnssec-signzone [-N increment] zonefile
```

The -N increment flag automatically increments the serial number in the SOA record so that you can't forget. You can also specify the value unixtime to update the serial number to the current UNIX time (seconds since January 1, 1970) or the value keep to prevent dnssec-signzone from modifying the original serial number. The serial number is incremented in the signed zone file but not in the original zone file.

Here's a spelled-out example that uses the keys generated above:

```
$ sudo dnssec-signzone -o example.com -N increment
-k Kexample.com+005+00682 example.com Kexample.com+005+23301
```

The signed file is sorted in alphabetical order and includes the DNSKEY records we added by hand and the RRSIG and NSEC records generated during signing. The zone's serial number has been incremented.

If you generated your keys with the NSEC3RSASHA1 algorithm, you would sign the zone as above but with the -3 salt flag.

Some other useful options to dnssec-signzone are

+   - -g to generate DS record(s) to be included in the parent zone
+   - -I to generate DLV record(s) for use if the parent zone is not signed
+   - -s start-time to set the time that the signatures become valid
+   - -e end-time to set the time that the signatures expire
+   - -t to print statistics

The dates for signature validity can be expressed as absolute times in the format yyyymmddhhmmss or as a time relative to now in the format +N, where N is in seconds. The default signature validity period is from an hour in the past to 30 days in the future. Here is an example in which we specify that signatures should be valid until the end of the calendar year 2010:

```
$ dnssec-signzone -N increment -e 20101231235959 example.com
```

Under NSD, the syntax for signing a zone is

```
ldns-signzone [-o zonename] zonename key [key ...]
```

You can just list both keys and let ldns-signzone figure out which is the KSK and which is the ZSK. For example:

```
$ sudo ldns-signzone example.com Kexample.com+005+00682 Kexample.com+005+23301
```

As with dnssec-signzone, you can use the -e yyyymmdd flag to set the expiration date for signatures. To generate NSEC3 records instead of NSEC records for signing gaps, use the flags -n -s salt.