
# 示例输入验证错误

```
#!/usr/bin/perl

open(HTMLFILE, "var/www/html/$ARGV[0]") or die "trying\n";

while(<HTMLFILE>) { print ; }

close HTMLFILE;
```
