Almost all DNS traffic uses the UDP transport, which we cover in Chapter 15, and is sent on port 53. We'll explain UDP and TCP and ports in Chapter 10. For now, if you want to trace only DNS traffic, you can instruct **tcpdump** to do so using a command like:

```
tcpdump -n port 53
```

For zone transfers, and if you use `nslookup`'s “-vc” option (“virtual circuit”), the DNS uses TCP instead of UDP. However, forget about that for now as we don't explain TCP and UDP until Chapters 10 and 15; we mention it here only for completeness.

# ## Appendices

+   - Appendix 6: making network settings permanent – Debian Linux
+   - Web Appendix 7: setting up a simple DNS server on Windows-NT
+   - Web Appendix 9: setting up a simple DNS server on Linux
+   - Web Appendix 10: sample DNS config files for a basic DNS server
+   - Web Appendix 11: name and domain registration