we would see the i-number 2 displayed for backups, because ls calls stat() to retrieve the i-node contents. We must do the same thing. We make several changes to make the program correct.

+   1. We replace get_ino() by a function, get_deviceid_inode() that gets the i-number and device-id for the given file name. We call this function when the program starts so that we have the device-id of the current working directory, and pass it to the recursive function, print_path().
+   2. We change the test within print_path() for when we have reached the root: we have reached the root if and only if the parent i-number matches the child i-number and they have the same device ids, otherwise we are not there yet.
+   3. We change the way we find the name of the current directory in inum_to_name(). We pass inum_to_name() the device-id and the i-number of the current working directory. inum_to_name() calls stat() for every entry in the current working directory, trying to match the i-number and the device-id stored in that entry's i-node against the i-number and device-d it was passed. If the i-number and device match the pair passed to inum_to_name(), then the d_name member of the dirent structure is the name of the current working directory, and this is what is returned to print_path().
+   4. To fix the problem with the terminating slash, which should not be at the end of the path, we can keep a static variable in the recursive function that keeps track of the level of recursion. The trailing slash will only be printed if we are in a recursive call, not at the top-level call.

All of these changes are incorporated into pwd2.c, whose code is below in Listing 2.

```
Listing 2. pwd2.c
// same includes as before

#define MAXPATH BUFSIZ

/**********************************************************/
void print_pwd ( char * abs_pathname );

// print_path prints to str the path from / to the file
// specified by cur_inum on the device with device id
// dev_num.
void print_path( char* str , ino_t cur_inum, dev_t dev_num);

// inum_to_name puts the filename of the file with inode inum
// on device with device number dev_num into string buf, at
// most len chars long and 0 terminates it.
void inum_to_name ( ino_t inum, dev_t dev_num,
    char * buf, int len );

// get_dev_ino gets the device id and the inode number of
// file fname, if that fname is the name of a file in the
// current working directory. Returns 0 if success, -1 if not.
int get_deviceid_inode ( const char *fname, dev_t *dev_id,
    ino_t *inum );
```