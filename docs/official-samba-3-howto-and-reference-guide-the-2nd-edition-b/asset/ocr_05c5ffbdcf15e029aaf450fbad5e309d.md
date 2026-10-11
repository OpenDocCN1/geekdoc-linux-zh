each and every diagnostic. At this stage your best bet is still to grep the source code and inspect the conditions that gave rise to the diagnostics you are seeing.

# TDB FILES

Samba stores it’s data in several TDB (Trivial Database) files, usually located in `/var/lib/samba`.

(*) information persistent across restarts (but not necessarily important to backup).

+   `account_policy.tdb*` NT account policy settings such as pw expiration, etc...

+   `broleck.tdb` byte range locks

+   `browse.dat` browse lists

+   `connections.tdb` share connections (used to enforce max connections, etc...)

+   `gencache.tdb` generic caching db

+   `group_mapping.tdb*` group mapping information

+   `locking.tdb` share modes & oplocks

+   `login_cache.tdb*` bad pw attempts

+   `messages.tdb` Samba messaging system

+   `netsamlogon.cache.tdb*` cache of user net_info.3 struct from net_samlogon() request (as a domain member)

+   `ntdrivers.tdb*` installed printer drivers

+   `ntforms.tdb*` installed printer forms

+   `ntprinters.tdb*` installed printer information

+   `printing/` directory containing tdb per print queue of cached lpq output