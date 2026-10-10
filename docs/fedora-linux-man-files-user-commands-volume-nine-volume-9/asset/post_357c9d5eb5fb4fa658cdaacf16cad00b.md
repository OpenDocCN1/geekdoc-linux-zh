
backing file to match the size of the smaller snapshot, you can safely truncate it yourself once the commit operation successfully completes.

The image *file1* is emptied after the operation has succeeded. If you do not need *file1* afterwards and intend to drop it, you may skip emptying *file1* by specifying the -d flag. If the backing chain of the given image file *file1* has more than one layer, the backing file into which the changes will be committed may be specified as *base* (which has to be part of *file1*’s backing chain). If *base* is not specified, the immediate backing file of the top image (which is *file1*) will be used. For reasons of consistency, explicitly specifying *base* will always imply -d (since emptying an image after committing to an indirect backing file would lead to different data being read from the image due to content in the intermediate backing chain overriding the commit target).

## **compare** [-f *fmt1*] [-F *fmt2*] [-T *src_cache*] [-p] [-s] [-q] *file1* *file2*

Check if two images have the same content. You can compare images with different format or settings.

The format is probed unless you specify it by -f (used for *file1*) and/or -F (used for *file2*) option.

By default, images with different size are considered identical if the larger image contains only unallocated and/or zeroed sectors in the area after the end of the other image. In addition, if any sector is not allocated in one image and contains only zero bytes in the second one, it is evaluated as equal. You can use Strict mode by specifying the -s option. When compare runs in Strict mode, it fails in case image size differs or a sector is allocated in one image and is not allocated in the second one.

By default, compare prints out a result message. This message displays information that both images are same or the position of the first different byte. In addition, result message can report different image size in case Strict mode is used.

Compare exits with 0 in case the images are equal and with 1 in case the images differ. Other exit codes indicate an error occurred during execution and standard error output should contain an error message. The following table summarizes all exit codes of the compare subcommand:

| Code | Description |
| :--- | :--- |
| 0 | Images are identical |
| 1 | Images differ |
| 2 | Error on opening an image |
| 3 | Error on checking a sector allocation |
| 4 | Error on reading data |

## **convert** [-c] [-p] [-n] [-f *fmt*] [-t *cache*] [-T *src_cache*] [-O *output_fmt*] [-o *options*] [-s *snapshot_id_or_name*] [-l *snapshot_param*] [-S *sparse_size*] *file1* [*file2* …] *output_file*

Convert the disk image *file1* or a snapshot

(snapshot_param(snapshot_id_or_name is deprecated) to disk image output_file using format output_fmt. It can be optionally compressed (-c option) or use any format specific options like encryption (-o option).

Only the formats qcow and qcow2 support compression. The compression is read-only. It means that if a compressed sector is rewritten, then it is rewritten as uncompressed data.

Image conversion is also useful to get smaller image when using a growable format such as qcow: the empty sectors are detected and suppressed from the destination image.

sparse_size indicates the consecutive number of bytes (defaults to 4k) that must contain only zeros for qe-img to create a sparse image during conversion. If *sparse_size* is 0, the source will not be scanned for unallocated or zero sectors, and the destination image will always be fully allocated.

You can use the *backing_file* option to force the output image to be created as a copy on write image of the specified base image; the *backing_file* should have the same content as the input's base image, however, the path, image format, etc may differ.

If the -n option is specified, the target volume creation will be skipped. This is useful for formats such as rbd if the target volume has already been created with site specific options that cannot be supplied through qe-img.

## **info [-f fmt] [--output=ofmt] [-backing-chain] file1**

Give information about the disk image *file1*. Use it in particular to know the size reserved on disk which can be different from the displayed size. If VM snapshots are stored in the disk image, they are displayed too. The command can output in the format *ofmt* which is either *human* or *json*.

If a disk image has a backing file chain, information about each disk image in the chain can be recursively enumerated by using the option –backing-chain.

For instance, if you have an image chain like:

```
base.qcow2 <- snap1.qcow2 <- snap2.qcow2
```

To enumerate information about each disk image in the above chain, starting from top to base, do:

```
qe-img info --backing-chain snap2.qcow2
```

## **map [-f fmt] [--output=ofmt] file1**

Dump the metadata of image *file1* and its backing file chain. In particular, this command dumps the allocation state of every sector of *file1*, together with the topmost file that allocates it in the backing file chain.

Two option formats are possible. The default format (human) only dumps known-nonzero areas of the file. Known-zero parts of the file are omitted altogether, and likewise for parts that are not allocated throughout the chain. **qe-img** output will identify a file from where the data can be read, and the offset in the file. Each line will include four fields, the first three of which are hexadecimal numbers. For example the first line of:

```
Offset Length Mapped to File
0 0x20000 0x50000 /tmp/overlay.qcow2
0x100000 0x10000 0x95380000 /tmp/backing.qcow2
```

/tmp/overlay.qcow2 (opened in raw format) starting at offset 0x50000 (327680). Data that is compressed, encrypted, or otherwise not available in raw format will cause an error if human format is in use. Note that file names can include newlines, thus it is not safe to parse this output format in scripts.

The alternative format `json` will return an array of dictionaries in JSON format. It will include similar information in the `start`, `length`, `offset` fields; it will also include other more specific information:

- whether the sectors contain actual data or not (boolean field `data`; if false, the sectors are either unallocated or stored as optimized all-zero clusters);
- whether the data is known to read as zero (boolean field `zero`);
- in order to make the output shorter, the target file is expressed as a depth; for example, a depth of 2 refers to the backing file of the backing file of `file1`.
  - In JSON format, the `offset` field is optional; it is absent in cases where human format would omit the entry or exit with an error. If `data` is false and the `offset` field is present, the corresponding sectors in the file are not yet in use, but they are preallocated.
  - For more information, consult `include/block/block.h` in QEMU's source code.

## **snapshot `[-l | -a] snapshot | -c snapshot | -d snapshot` `file1`**

List, apply, create or delete snapshots in image `file1`.

## **`rebase` `[-f fmt]` `[-t cache]` `[-T src_cache]` `[-p]` `[-u]` `-b` `backing_file` `[-F backing_fmt]` `file1`**

Changes the backing file of an image. Only the formats `qcow2` and `qed` support changing the backing file.

The backing file is changed to `backing_file` and (if the image format of `file1` supports this) the backing file format is changed to `backing_fmt`. If `backing_file` is specified as `""` (the empty string), then the image is rebased onto no backing file (i.e. it will exist independently of any backing file).

`cache` specifies the cache mode to be used for `file1`, whereas `src_cache` specifies the cache mode for reading backing files.

There are two different modes in which `rebase` can operate:

### Safe mode

This is the default mode and performs a real rebase operation. The new backing file may differ from the old one and `qe-img` rebase will take care of keeping the guest-visible content of `file1` unchanged.

In order to achieve this, any clusters that differ between `backing_file` and the old backing file of `file1` are merged into `file1` before actually changing the backing file. Note that the safe mode is an expensive operation, comparable to converting an image. It only works if the old backing file still exists.
