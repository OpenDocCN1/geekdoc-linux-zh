included in the executable file by default can be stripped out to make the executable file smaller.

To determine whether symbols are present in one of your executable files, Unix the nm utility on that file:

nm hilinux

No one's ever explained to what nm stands for, my hunch is it's a scrunched form of “name.” (When it was created, people communicated with Unix electromechanical Teletype machines, which were ponderously slow and difficult to type on. There was a big payback in using short names for things.) What you'll see when you run nm will either be a list of symbols, or else this message:

hilinux: no symbols

The list, when you get one, will be quite long—and most of the symbols on the list will be unfamiliar to you. That's because they're symbols of elements of the C library that have been linked into your program. Your symbols, the ones defined in your assembly language program, will be somewhere—alas, they're not all conveniently together. Look for main—assuming you defined a label main in your program (and you most will have trouble linking it with the C library), there will be, probably near the end of the list. Here's a typical nm list for a very simple program that I present in the next chapter:

```
0804943c ? _DYNAMIC
08049420 ? _GLOBAL_OFFSET_TABLE_
080483fc R _IO_strdin_used
08049414 ? _CTOR_END_
08049410 ? _CTOR_LIST_
0804941c ? _DTOR_END_
08049418 ? _DTOR_LIST_
0804940c ? _EH_FRAME_BEGIN_
0804940c ? _FRAME_END_
080494dc A _bss_start
08049400 D _data_start
U _deregister_frame_info@GLIBC_2.0
080483b0 t _do_global_ctors_aux
08048320 t _do_global_dtors_aux
U _gmon_start_
U _libc_start_main@GLIBC_2.0
U _register_frame_info@GLIBC_2.0
080494dc A _edata
08049f4 A _end
080483dc A _etext
080483dc ? _fini
```