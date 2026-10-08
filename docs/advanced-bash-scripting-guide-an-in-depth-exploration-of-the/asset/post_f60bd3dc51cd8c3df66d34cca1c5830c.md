
# Advanced Bash-Scripting Guide

the Field-Array-Name:
Index-Array-Name[Line-Number * 2] : The "inode" field element.
NOTE: This distance may be +11 or +12 elements.
Index-Array-Name[(Line-Number * 2) + 1] : The "pathname" element.
NOTE: This distance may be a variable number of elements.
Next line index pair for Line-Number+1.
IndexList()

```bash
IndexList() {
    local -a INDEX=( 0 0 )
    local -i LidxCnt
    local -i if=0 # Default to variable names

    case "#" in # Simplistic option testing
        0) return 1;
        1) return 1;
        2) ;;
        3) case "$1" in # Poor man's continue
            -if) if=1;
            -of) of=1;
            *) return 1;
        esac; shift;
        4) if=1; of=1; shift; shift;
        *) return 1
    esac
```

# A little elegance here would handle pipes,
++ sockets, deleted files - later.

# Appendix A Contributed Scripts

```bash
*)
  until IsNumber ${LIST[$Lidx]} || ((Lidx >= Lcntn))
  do
    ((Lidx+=1))
  done
  esac
  # Not required
INDEX[$#INDEX[@]]=$inode
INDEX[$#INDEX[@]]=$name
INDEX[0]=$INDEX[0]+1
  # One more "line" found
echo "Line: ${INDEX[0]} Type: $ft Links: $m inode \"
  $ ${LIST[$inode]} Name: ${LIST[$name]}"
```

```bash
else
  ((Lidx+=1))
fi
  case "$of" in
    0) eval $2="\${INDEX[$#}]}" \;;
    1) echo "${INDEX[$0]}" > "$2"
  esac
```

```bash
return 0
# What could go wrong?
```

# Identify File
# Digest Input-Array-Name
# or
# Here document used as a comment block.
StatFields:
The key (no pun intended) to Unified File System (UCFS) is to distinguish files based on their content. Distinguishing files by their name is just so. The content is distinguished by computing a checksum of that content. This uses the mdsum program to generate a 128-bit representative of the file's content. There is a chance that two files having different content might generate the same checksum using mdsum (or any checksum). Should that become a problem, then the use of mdsum can be replaced by a cryptographic signature. But... the mdsum program is documented as outputting three fields (and it does), but it appears as two fields (array). This is caused by the lack of whitespace between the second and third field. So this function grooms the mdsum output and returns

[0] 32 characters (filename)
[1] text file
[2] binary file
Note: That name may be the STDIN read.

```bash
DigestFile(){
  local if=0 # Default, variable name
  local -a T1 T2
```

```bash
case "$#" in
  3) case "$1" in
      -if) if=1; shift;
      esac
  2) :; # Poor man's "continue"
      return 1;;
  esac
```

```bash
case $if in
  0) eval T1=$(echo ${T1[0]} | md5sum)
      ;;
  1) T2=$(md5sum $1)
      ;;
esac
```

```bash
case ${T2[@]} in
  0) return 1;;
  1) return 1;;
  2) case ${T2[1]} in # Script-2.0.5
      ${T2[@2]}=T2[1]}
      ;;
  3) :; # Assume it worked
      return 1;;
esac
```

```bash
local -i len=${T2[0]}
if [ $len -ne 32 ]; then return 1; fi
eval T2="${T2[1]}"
```

# #### Locate File

# FileName Location-Array-Name
# #### A file location is Filesystem-id and inode-number

# Here document used as a comment block.
StatFields:
Based on stat, version 2.2
stat -t and stat -lt fields

[0] name
[1] Total size - number of bytes
[2] Symbolic link length of pathname
[3] Number of (2 byte) blocks allocated
[4] File type and access rights (hex)
[5] User ID of owner
[6] Group ID of owner
[7] Device number
[8] Inode number
[9] Number of hard links
[10] Device type (if inode device) Major
[11] Device type (if inode device) Minor
[12] Time of access
May be disabled in 'mount' with noatime
atime of files changed by exec, read, pipe, truncate, inode (mmap?)
atime of directories changed by addition/deletion of files
[13] Time of last modification
time of files changed by write, truncate, inode
time of directories changed by addition/deletion of files
[14] Time of last change
ctime reflects time of changed inode information (owner, group) permissions, link count

```
Per:
Return code: 0
Size of array: 14
Contents of array
Element 0: /home/mszick
Element 1: 4096
Element 2: 8
Element 3: 418
Element 4: 500
Element 5: 500
Element 6: 603
Element 7: 32385
Element 8: 22
Element 9: 0
Element 10: 0
Element 11: 1051221030
Element 12: 1051214068
Element 13: 1051214068
```

```
For a link in the form of linkname -> realname
stat -t linkname returns the linkname (link) information
stat -lt linkname returns the realname information
```

```bash
stat -tf and stat -lt fields
[0] name
[1] ID-0: Maybe someday, but Linux structure
[2] ID-0: does not have either information, currently must come from file-specific utilities. These will be munged into:
[1] Volume label if possible
[2] Volume label if possible
Note: 'mount -l' does return the label and could return
[3] Maximum length of filenames
[4] Filesystem type
[5] Total blocks in the filesystem
[6] Free blocks for non-root users
[7] Free blocks of the filesystem
[8] Block size of the filesystem
[9] Total inodes
[10] Free inodes

```
Per:
Return code: 0
Size of array: 14
Contents of array
Element 0: /home/mszick
Element 1: 0
Element 2: 0
Element 3: 255
Element 4: 0
Element 5: 258145
Element 6: 227180
Element 7: 214650
Element 8: 4096
Element 9: 131152
Element 10: 127625
```

```bash
# FileName Location-Array-Name
LocateFile()
{
    local -a LOC1 LOC2
    local lm="of=0

    case "$#" in
        0) return 1 ;;
        1) return 1 ;;
        2) while (( "$#" > 2 ))
        do
            case "$1" in
                -1) lk=-1 ;;
                -of) of=1 ;;
            esac
            shift
        done
        return 1 ;;
    esac
```

# More Script-2.0.5
LOC1=$($stat -t $lk)
LOC2=$($stat -of $lk)
# Uncomment above lines if system has "stat" command.
LOC=(${LOC1[0]:11} ${LOC1[3]:2} ${LOC2[1]:4})

case "$#" in
    0) eval $2="${LOC[0]}" ;;
    1) echo "${LOC[0]}" > "$2"
esac
return 0

# Which yields (if you are lucky), have "stat" installed
# Descriptor
Return code: 0
Size of array: 15
Contents of array
Element 0: /home/mszick
Element 1: 418
Element 2: 500
Element 3: 500
Element 4: 403
Element 5: 3385
Element 6: 22
Element 7: 0
Element 8: 0
Element 9: 1051224068 Access
Element 10: 1051224068 Modify
Element 11: 1051224068 Status
Element 12: 0 UUID (to be)
Element 13: 0 Volume Label (to be)
Element 14: ef53 Filesystem type
}

And then were some test code

```bash
declare -a CUR_DIR
# For small arrays
ListDirectory "${PWD}" CUR_DIR
ListArray CUR_DIR
```

```bash
declare -a DIR_DIG
DigestFile CUR_DIR_DIG_IND
echo "The name (checksum) for ${CUR_DIR[9]} is ${DIR_DIG[0]}"
```

```bash
declare -a DIR_ENT
# For really big arrays - use a temporary file in ramdisk
# ListDirectory "${CUR_DIR[11]}"/* /tmp/junk2
ListDirectory "${CUR_DIR[11]}/* DIR_ENT
```

```bash
declare -a DIR_IDX
# Indexlist -if "/tmp/junk2" DIR_IDX
ListIndex DIR_ENT_DIR_IND
```

```bash
declare -a IDX_DIG
# DIR_ENT=$(cat /tmp/junk2)
# getfile -if "/tmp/junk2" IDX_DIG
DigestFile IDX_ENT_DIG_IND
# Small (should) be able to parallelize Indexlist & DigestFile
# Large (should) be able to parallelize Indexlist & DigestFile & the assignment
echo "The name (checksum) for the contents of ${PWD} is ${IDX_DIG[0]}"
```

```bash
declare -a FILE_LOC
LocateFile "${PWD}" FILE_LOC
ListArray FILE_LOC
```

exit 0
Stephane Chazelas demonstrates object-oriented programming in a Bash script.

Appendix A. Contributed Scripts
