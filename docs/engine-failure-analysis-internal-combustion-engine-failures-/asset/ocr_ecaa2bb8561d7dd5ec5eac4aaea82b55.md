# OPTIONS (*CONT.*)

+   - **-s, --swap-bytes**:  Swap the bytes of each pair of bytes.  *Mode: Copy-in.*
+   
+   - **-S, --swap-halfwords**: Swap the half words of each word.  *Mode: Copy-in.*
+   
+   - **--sparse**: Use the sparse file format to reduce the size of files with large blocks of zeroes.  *Modes: Copy-out, pass-through.*
+   
+   - **-t, --list**: Display a list of filenames instead of copying the files.  *Modes: Copy-out, copy-in, pass-through.*
+   
+   - **-u, --unconditional**: Replace all existing files without confirmation.  *Modes: Copy-in, pass-through.*
+   
+   - **-v, --verbose**: Display filenames while they are processed.  *Modes: Copy-out, copy-in, pass-through.*
+   
+   - **-V, --dot**: Display a progress bar that uses dots to show each file that is processed.  *Modes: Copy-out, copy-in, pass-through.*
+   
+   - **--version**: Display the version number.  *Modes: Copy-in, copy-out, pass-through.*

# EXAMPLES

+   - **`ls | cpio -ov > my_directory`**: Creates an archive with the specified filename (*this-directory.cpio*) that contains all the files in the working directory.