```
% touch file.1
%
```

2. Delete the everyone@ entry in the ACLs for file.1:

```
% setfacl -x everyone@:r-----a-R-c-s------:allow file.1
% getfacl file.1
# file: file.1
# owner: bob
# group: bob
    owner@:rw-p--aARWcCos:------:allow
    group@:r-----a-R-c-s------:allow
```

3. Add a new everyone@ entry. Notice the -m option places the new entry at position 0:

```
% setfacl -m everyone@:r-----a-R-c-s------:allow file.1
% getfacl file.1
# file: file.1
# owner: bob
# group: bob
    everyone@:r-----a-R-c-s------:allow
    owner@:rw-p--aARWcCos:------:allow
    group@:r-----a-R-c-s------:allow
```

4. Delete file.1 and create a new version of it with the default ACLs:

```
% rm file.1
% touch file.1
% getfacl file.1
# file: file.1
# owner: bob
# group: bob
    owner@:rw-p--aARWcCos:------:allow
    group@:r-----a-R-c-s------:allow
    everyone@:r-----a-R-c-s------:allow
```

5. Modify the position 2 everyone@ entry to rw only:

```
% setfacl -m everyone@:rw:allow file.1
% getfacl file.1
# file: file.1
# owner: bob
# group: bob
```