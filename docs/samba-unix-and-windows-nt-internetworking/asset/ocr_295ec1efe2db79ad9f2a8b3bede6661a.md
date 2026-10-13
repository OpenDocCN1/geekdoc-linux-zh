# File Name Mangling

Along with the mapping of access control attributes and permissions, Samba also translates file and path names into their respective UNIX, DOS, and Windows forms (Table 11.2). In general, the translation entails applying an algorithm (Table 11.4) to convert long case-sensitive UNIX file names into case-insensitive DOS 8.3 format. The method is similar to, but different from, that employed by Windows 9x and Windows NT when transforming long file names (LFN) into a DOS 8.3 representation. The ability of a client to support LFN or DOS 8.3 format is negotiated during session setup.

# Table 11.2 File Name Characteristics

| Category | Details |
|---|---|
| UNIX | File name 255 chars; All chars except "/" and ESC; Mixed case, case sensitive |
| DOS (pre 7.0), Windows for Workgroups | File name 8.3 chars; All chars except \ / : * ? " < > |; Upper case translation, case insensitive |
| Windows 9x, Windows NT | File name 127 chars; All chars except \ / : * ? " < > |; Win32, LFN, Universal Naming Convention (UNC) names |