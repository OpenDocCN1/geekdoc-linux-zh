
## B.1.4 BIT Type

`BIT`[`M`]

**Meaning.** A bit-field value. M should be an integer from 1 to 64 indicating the number of bits per value. If omitted, M defaults to 1.

**Allowable attributes.** None, other than the global attributes

**Default value.** NULL or the column can be NULL, 0 if NOT NULL

**Storage required.** Approximately (M+7)/8 bytes.

**Note.** The BIT type was introduced as a separate data type in MySQL 5.0.3. Initial BIT support was limited to MyISAM; this was extended to InnoDB, MEMORY, and ARCHIVE in 5.0.5, and to Falcon in MySQL 6.0. Prior to 5.0.3, BIT is a synonym for TINYINT(1).

## B.2 String Types

The MySQL string types are general-purpose types and commonly are used to store binary or character (text) data. Types are available to hold values of varying maximum lengths and can be chosen according to whether you want values to be treated as binary or non-binary strings.

BINARY, VARBINARY, and the BLOB types are binary string types. A binary string is a sequence of bytes, and its length is measured in bytes. Binary strings have no character set and values are compared based on their numeric byte values.

CHAR, VARCHAR, and the TEXT types are non-binary string types. A non-binary string is a sequence of characters. It has a character set and collation. The character set defines the allowable characters for the data type and the collation defines the character sort order. A length as specified in a non-binary string column definition indicates how many characters you want the column to be able to hold.

Lengths of non-binary string values normally are measured in characters but can be measured in bytes instead. To obtain the length of a non-binary string in characters or bytes, use the CHAR_LENGTH() or LENGTH() function, respectively. A non-binary string that is n characters long is also n bytes long if it contains single-byte characters, but more than n bytes long if it contains multi-byte characters. This affects the storage requirements for non-binary string columns:

- Fixed-length columns such as CHAR(M) require enough space to store M instances of the widest character in the character set. For example, characters in the utf8 character set vary from one to three bytes each, so CHAR(M) requires M × 3 bytes. (In MySQL 6.0.4 and up, utf8 characters can require up to four bytes.)
- Variable-length columns such as VARCHAR(M) require only enough space to store the actual characters in a given value, plus the prefix that stores the value’s length in bytes. A VARCHAR(10) column with the double-byte utf8 character set requires one byte for the length prefix, plus anywhere from 0 bytes for an empty string to 20 bytes for a 10-character string.

You can specify a character set and collation for the non-binary string types (CHAR, VARCHAR, TEXT), as well as for the ENUM and SET types:

- The syntax for specifying a character set is CHARACTER SET charset, where charset is a character set name such as latin1, greek, or utf8. CHARSET is a synonym for CHARACTER SET.
- The syntax for specifying a collation is COLLATE collation, where collation names one of the allowable collations for the character set.
- If no character set or collation are given, they are determined from the table defaults. If a character set is given without a collation, the collation is the default collation for the character set. If a collation is given without a character set, the character set is implied by the collation name. If a character set and collation both are given, the collation must be compatible with the character set. For example, the latin1_bin collation is compatible with latin1 but not with utf8.
- The binary character set and the BINARY column attribute are treated specially:
    - If you specify CHARACTER SET binary for a non-binary string type, it causes conversion to the corresponding binary string type. That is, CHAR becomes BINARY, VARCHAR becomes VARBINARY, and the TEXT types become BLOB types. ENUM and SET have no corresponding binary types, so CHARACTER SET binary simply becomes a column attribute as is.
    - The BINARY attribute is equivalent to specifying the binary collation for the character set (the collation name that ends with _bin). For example, a column defined as CHAR(10) CHARACTER SET utf8 BINARY becomes CHAR(10) CHARACTER SET utf8 COLLATE utf8_bin.
- For non-binary string types, the ASCII and UNICODE attributes are shorthand for CHARACTER SET latin1 and CHARACTER SET ucs2, respectively.

The allowable character sets and collations supported by the server can be determined by issuing the SHOW CHARACTER SET and SHOW COLLATION statements. These statements show which collation is the default for each character set. You can also examine the CHARACTER_SETS and COLLATIONS tables in the INFORMATION_SCHEMA database, which contain equivalent information.

Handling of values that are too long to be stored in a string column is dependent on the SQL mode value. If strict mode is not enabled, values are chopped to fit. Also, a warning is generated unless the chopped characters are spaces. In strict mode, an error occurs and no value is inserted if non-space characters must be chopped.

Handling of trailing pad values varies for different string types:
- For CHAR, values are padded with spaces if necessary to the column length when stored. Trailing spaces are removed when values are retrieved.
- For BINARY, values are padded with 0x00 bytes if necessary to the column length when stored. Nothing is removed when values are retrieved. (Before MySQL 5.0.15, BINARY values are padded with spaces when stored, and trailing spaces are removed on retrieval.)
- For VARBINARY and VARCHAR, no padding is added or removed when values are stored or retrieved. (Before MySQL 5.0.3, trailing spaces are removed when values are stored.)
- For the BLOB and TEXT types, no pad values are added or removed for storage or retrieval.
- For ENUM and SET, any trailing spaces in member values listed in the column definition are ignored. Consequently, any trailing spaces are stripped from values stored in the column because MySQL converts each value to the corresponding internal numeric value of the column member. This affects comparisons as well, in that trailing spaces are not significant in values compared to ENUM or SET columns.

### B.2.1 Binary String Types

`BINARY[ M ]`

**Meaning.** A fixed-length binary string 0 to *M* bytes long. *M* should be an integer from 0 to 255. If omitted, *M* defaults to 1.

**Allowable attributes.** None, other than the global attributes

**Allowable length.** 0 to *M* bytes

**Default value.** NULL if the column can be NULL, '' (empty string) if NOT NULL

**Storage required.** *M* bytes

**Comparisons.** Byte by byte, based on numeric byte values

`VARBINARY( M )`

**Meaning.** A variable-length binary string 0 to *M* bytes long. *M* should be an integer from 0 to 65535 (0 to 255 prior to MySQL 5.0.3).

**Allowable attributes.** None, other than the global attributes

**Allowable length.** 0 to *M* bytes

**Default value.** NULL if the column can be NULL, '' (empty string) if NOT NULL

**Storage required.** Length of value (in bytes), plus a 1-byte or 2-byte prefix to record the length. The prefix requires 1 byte if the maximum length of column values in bytes is less than 256, 2 bytes otherwise.

**Comparisons.** Byte by byte, based on numeric byte values

Note. In practice, the maximum length of a VARBINARY column may be less than 65535 bytes, depending on storage engine internal row-size limits and the space required by other columns in the table.

`TINYBLOB`

**Meaning.** A small BLOB (binary string) value

`BLOB(*M*)`

**Meaning.** A normal-sized BLOB (binary string) value

**Allowable attributes.** None, other than the global attributes

**Allowable length.** 0 to 65535 (0 to 2<sup>16</sup>-1) bytes. If a length *M* is given, it is used to choose the appropriate data type and then discarded. For lengths of 1 to 65535, the data type becomes BLOB. For lengths of 65536 or greater, the data type becomes whichever of MEDIUMBLOB or LONGBLOB is required to accommodate values of the given length.

**Default value.** NULL if the column can be NULL, '' (empty string) if NOT NULL

**Storage required.** Length of value (in bytes), plus 2 bytes to record the length

**Comparisons.** Byte by byte, based on numeric byte values

`MEDIUMBLOB`

**Meaning.** A medium-sized BLOB (binary string) value

**Allowable attributes.** None, other than the global attributes

**Allowable length.** 0 to 16777215 (0 to 2<sup>24</sup>-1) bytes

**Default value.** NULL if the column can be NULL, '' (empty string) if NOT NULL

**Storage required.** Length of value (in bytes), plus 3 bytes to record the length

**Comparisons.** Byte by byte, based on numeric byte values

**Synonyms.** LONG VARBINARY

`LONGBLOB`

**Meaning.** A large BLOB (binary string) value

**Allowable attributes.** None, other than the global attributes

**Allowable length.** 0 to 4294967295 (0 to 2<sup>32</sup>-1) bytes

**Default value.** NULL if the column can be NULL, '' (empty string) if NOT NULL

**Storage required.** Length of value (in bytes), plus 4 bytes to record the length

**Comparisons.** Byte by byte, based on numeric byte values
