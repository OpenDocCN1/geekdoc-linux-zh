backing file to match the size of the smaller snapshot, you can safely truncate it yourself once the commit operation successfully completes.

The image *filena* is emptied after the operation has succeeded. If you do not need *filena* afterwards and intend to drop it, you may skip emptying *filena* by specifying the -d flag. If the backing chain of the given image file *filena* has more than one layer, the backing file into which the changes will be committed may be specified as *base* (which has to be part of *filena*’s backing chain). If *base* is not specified, the immediate backing file of the top image (which is *filena*) will be used. For reasons of consistency, explicitly specifying *base* will always imply -d (since emptying an image after committing to an indirect backing file would lead to different data being read from the image due to content in the intermediate backing chain overriding the commit target).

# **compare** [-f *fmt1*] [-F *fmt2*] [-T *src_cache*] [-p] [-s] [-q] *filena1* *filena2* Check if two images have the sa content. You can compare images with different format or settings.

The format is probed unless you specify it by -f (used for *filena1*) and/or -F (used for *filena2*) option.

By default, images with different size are considered identical if the larger image contains only unallocated and/or zeroed sectors in the area after the end of the other image. In addition, if any sector is not allocated in one image and contains only zero bytes in the second one, it is evaluated as equal. You can use Strict mode by specifying the -s option. When compare runs in Strict mode, it fails in case image size differs or a sector is allocated in one image and is not allocated in the second one.

By default, compare prints out a result sgage. This sgage displays information that both images are sa or the position of the first different byte. In addition, result sgage can report different image size in case Strict mode is used.

Compare exits with 0 in case the images are equal and with 1 in case the images differ. Other exit codes an an error occurred during execution and standard error output should contain an error sgage. The following table summarizes all exit codes of the compare subcommand:

+   - 0
+   	Images are identical

+   - 1
+   	Images differ

+   - 2
+   	Error on opening an image

+   - 3
+   	Error on checking a sector allocation

+   - 4
+   	Error on reading data

# **convert** [-c] [-p] [-n] [-f *fmt*] [-t *cache*] [-T *src_cache*] [-O *output_fmt*] [-o *options*] [-s *snapshot_id_or_na*] [-l *snapshot_param*] [-S *sparse_size*] *filena* [*filena2* …]] *output_filena* Convert the disk image *filena* or a snapshot