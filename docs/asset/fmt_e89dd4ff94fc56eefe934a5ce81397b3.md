
195.175 139.86 <SMALL eth> 240 140 140 195.176 139.87 <n WITH TILDE> 241 73 73 177.198 <WITH GRAVE> 242 205 205 197.
139.89 <WITH ACUTE> 243 206 206 195.179.198 <WITH CIRCUMLEX> 244 203 203 195.130.199 <WITH TILDE> 245 207 207 207.181
139.100 <WITH DIERESIS> 246 204 204 194.182 <DIVISION SIGN> 247 225 225 225 193.182.190 <WITH STROKE> 248 112 112 112.184
139.23 <WITH DIERESIS> 249 221 221 195.185.194 <WITH ACUTE> 250 222 222 222 195.186.195 <WITH CIRCUMLEX> 251 219 219 219.187
139.105 <WITH DIERESIS> 252 220 220 220 195.188.139.12 <WITH ACUTE> 253 141 141 141 195.189 139.113 <SMALL LETTER thorn> 254 142 142 142
195.190 139.114 <WITH DIERESIS> 255 223 223 225 239.191 139.115

如果你在 CCID 0037 顺序中看到了 ASCII+ Latin-1 中的数字 36 的变化，请运行以下命令：

# 配方 4

```perl
perl -ne 'if/(.{29}\d{1,3}\s{2,4}\d{1,3}\s{2,4}\d{1,3})\/'
-e 'push(@$_);' -e END(print map{$_->[0]})' -e sort{$a->[1]} <=
$b->[1]}' -e map{[$,substr($_,44,33)]@{1}; perbcid.com
```

如果你在 CCID 0037 顺序中看到了最后一行数字 36 的变化：

# 配方 5

```perl
perl -ne 'if/(.{29}\d{1,3}\s{2,4}\d{1,3}\s{2,4}\d{1,3})\/'
-e 'push(@$_$_),' -e END(print map{$_->[0]})' -e sort{$a->[1]} <=
$b->[1]}' -e map{[$,substr($_,44,39)]@{1}; perbcid.com
```

如果你在 POSIX-base 变化中看到了变化，请将最后一行的数字 34 改为 44，如下所示：

# 配方 6

```perl
perl -ne 'if/(.{29}\d{1,3}\s{2,4}\d{1,3}\s{2,4}\d{1,3})\/'
-e 'push(@$_),' -e END(print map{$_->[0]})' -e sort{$a->[1]} <=
$b->[1]}' -e map{[$,substr($_,44,33)]@{1}; perbcid.com
```
