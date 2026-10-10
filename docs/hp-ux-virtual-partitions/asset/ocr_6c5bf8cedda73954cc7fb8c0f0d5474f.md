_st_fail_overruns_

If set, SCSI tape read resulting in data overrun causes failure.

Acceptable Values:

+   Disabled: ``0``
+   Enabled: ``1``
+   Default: ``0``

Specify ``0`` or ``1``.

Description

Certain technical applications depend on the fact that reading a record smaller than the actual tape record size should generate an error.

_st_large_recs_

If set, enables large record support for SCSI tape.

Acceptable Values:

+   Disabled: ``0``
+   Enabled: ``1``
+   Default: ``0``

Specify ``0`` or ``1``.

Description

This parameter is used in conjunction with
``scsi_maxphys`` to enable large tape record support without logical record breakup and recombination.

_scroll_lines_

Specify the number of display lines in ITE console screen buffer.

Acceptable Values:

+   Minimum: ``60``
+   Maximum: ``999``