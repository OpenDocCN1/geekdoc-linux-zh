

## 3.10.5 获取链接引用的名称

如果文件是一个符号链接，我们需要打印出它指向的文件的路径名。如果我们对可能处理链接的函数进行 manpage 搜索，即

```
man -k link | grep '([23])'
```

我们会看到，在一组选项中，有

```
readlink (2)      - read value of a symbolic link
```

这显然是我们需要的。阅读其 manpage 我们看到 readlink() 函数读取链接的值：

```
SYNOPSIS
    #include <unistd.h>
    ssize_t readlink(const char *path, char *buf, size_t bufsiz);
Feature Test Macro Requirements for glibc (see feature_test_macros(7)):
    readlink(): _BSD_SOURCE || _XOPEN_SOURCE >= 500 || _POSIX_C_SOURCE >= 200112L

DESCRIPTION
    readlink() places the contents of the symbolic link path in the buffer buf, which has size bufsiz. readlink() does not append a null byte to buf. It will truncate the contents (to a length of bufsiz characters), in case the buffer is too small to hold all of the contents.
```

readlink() 用符号链接 path 的内容填充其第二个参数。此存储由调用程序分配，而不是由 readlink() 分配，因此你需要声明一个足够大的字符串来容纳路径名。你可以将其声明为大小为 PATH_MAX，但这会非常大，如果名称非常大，最好将其截断。因为 readlink() 不会在字符串末尾附加空字节，该函数的正确用法大致如下，如果 filename 是正在读取的链接：

```
ssize_t count;
if ( -1 == (count = readlink(filename, buf, NAME_MAX-1)) )
    perror("function calling this ");
else {
    buf[count] = '\0';
    // use the buf contents here
}
```

NAME_MAX 是文件名的最大长度，通常约为 255。这也可能太大了。

第二个版本的 ls 如下。此版本仍然不解析命令行以检测是否出现了 -l 选项，但代码已修改以便以后轻松加入该更改。其他缺陷在列表之后说明。

> 12 回顾第 1 章，PATH_MAX 是一个系统相关的限制，指定路径名中的最大字节数。

### Listing ls.c Version 2
```
void print_file_status( char *, struct stat *);
void mode2str( int , char [] );
char * get_date_no_day( time_t * time );
char * uid2name( uid_t );
char * gid2name( gid_t );
void ls(char [], int);

int main(int argc, char *argv[])
{
    int i = 1;

    if ( argc == 1 )    // no arguments; use .
        ls( HERE );
    else
        while ( i < argc ){
            printf("%s:\n", argv[i]);
            ls( argv[i], 1 );
            i++;
        }
}

// Does not check whether entries are files or directories
// or . files
void ls( char dirname[], int do_longlisting )
{
    DIR           *dir_ptr;    // directory stream
    struct dirent *direntp;    // holds one entry
    struct stat   info;        // stores stat results

    if ( ( dir_ptr = opendir( dirname ) ) == NULL )
        // could not open — maybe it was not a directory
        fprintf(stderr,"ls1: cannot open %s\n", dirname);
    else {
        while ( ( direntp = readdir( dir_ptr ) ) != NULL ) {
            if ( do_longlisting ) {
                if ( lstat(direntp->d_name, &statbuf) == -1 ) {
                    perror(direntp->d_name);
                    continue; // stat call failed but we go on
                }
                print_file_status(direntp->d_name, &statbuf);
            }
            else // not long — just print name
                printf("%s\n", direntp->d_name);
        }
        closedir(dir_ptr);
    }
}

void print_file_status( char *filename , struct stat *info_p )
{
    char      modestr[11];
    ssize_t count;
    char      buf[NAME_MAX];
```

```
mode2str( info_p->st_mode, modesstr );
printf ( "%s" , modesstr );
printf ( "%4d " , (int) info_p->st_nlink);
printf ( "%-8s " , uid2name(info_p->st_uid) );
printf ( "%-8s " , gid2name(info_p->st_gid) );
printf ( "%8ld " , (long)info_p->st_size );
printf ( "%12s " , get_date_no_day(info_p->st_mtime));
printf ( "%s" , filename );
if ( S_ISLNK(info_p->st_mode) ) {
    if ( -1 == (count = readlink(filename, buf, NAME_MAX-1)) )
        perror("print_file_status: ");
    else {
        buf[count] = '\0';
        printf("-->%s", buf);
    }
}
printf("\n");
}

// Given user-id, return user-name if possible
char *uid2name ( uid_t uid )
{
    struct passwd *pw_ptr;
    static char numstr[10];  // must be static!

    if ( ( pw_ptr = getpwuid( uid ) ) == NULL ) {
        // convert uid to a string; using sprintf is easiest
        sprintf(numstr,"%d", uid);
        return numstr;
    }
    else
        return pw_ptr->pw_name;
}

char *gid2name ( gid_t gid )
{
    struct group *grp_ptr;
    static char numstr[10];

    if ( ( grp_ptr = getgrgid(gid) ) == NULL ) {
        // convert gid to string
        sprintf(numstr,"%d", gid);
        return numstr;
    }
    else
        return grp_ptr->gr_name;
}
```

## What Is Still Wrong?

- 它仍然将所有参数都当作目录处理，如果给出普通文件则显示错误。

