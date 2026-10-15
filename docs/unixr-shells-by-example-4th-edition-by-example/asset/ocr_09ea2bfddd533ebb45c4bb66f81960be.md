Archie McNichol--(206) 548-1348
Guy Quigley--(916) 343-6410
Dan Savage--(406) 298-7744
Tom Savage--(408) 926-3456
Elizabeth Stachelin--(916) 440-1763
Thanks to all of you for your continued support!!

# 6.25 Odds and Ends

Some data (e.g., that read in from tape or from a spreadsheet) may not have obvious field separators but may instead have fixed-width columns. To preprocess this type of data, the substr function is useful.

# 6.25.1 Fixed Fields

In the following example, the fields are of a fixed width, but are not separated by a field separator. The substr function is used to create fields.

# EXAMPLE 6.167

```
% cat fixed
031291ax5633(408)987-0124
021589bg2455(415)866-1345
122498de1227(916)933-1234
010187ax3458(408)264-2546
092491bd9923(415)1234-8900
112990bg4567(803)234-1456
070489qr3455(415)899-1426
```

```
% nawk '{printf substr($0,1,6) " ";printf substr($0,7,6) " ";\nprint substr($0,13,length())}' fixed
031291 ax5633 (408)987-0124
021589 bg2455 (415)866-1345
122490 de1237 (916)933-1234
010187 ax3458 (408)264-2546
092491 bd9923 (415)1234-8900
112990 bg4567 (803)234-1456
070489 qr3455 (415)899-1426
```

# EXPLANATION

The first field is obtained by getting the substring of the entire record, starting at the first character, offset by 6 places. Next, a space is printed. The second field is obtained by getting the substring of the record, starting at position 7, offset by 6 places, followed by a space. The last field is obtained by getting the substring of the entire record, starting at position 13 to the position represented by the length of the line. (The length function returns the length of the current line, $0, if it does not have an argument.)