# # National Language Support 8

> > Anybody who has a mail gateway that isn't 8-bit clean these days should be shot.
Linus Torvalds

The UNIX operating system was developed in the USA. Therefore, practically all available UNIX systems and programs use (American) English as the language for messages, menus, and documentation, and the (US-) ASCII character set for the interpretation of character strings and processing of texts.

The same can be said for LINUX which was developed as a UNIX-compatible system by an international community of programmers, using many of the existing UNIX programs.

For a worldwide diffusion of UNIX and LINUX it is necessary to remove these implicit dependencies and make them configurable for the user. This is achieved by means of *National Language Support* (NLS). The aim is to make a UNIX system behave as if it had been specially developed for the linguistic and cultural environment of the user.

The general support of NLS is also known as *internationalization*, whereas the translation of texts into a specific language and the adaptation of the system to a specific cultural environment is *localization*.

The following pages briefly describe the POSIX standard as far as it describes functions of the NLS. The emphasis lies on a general introduction to the terms and capabilities of the NLS, to give system administrators and users an idea of multi-language UNIX and LINUX operating systems.

Chapter 9 (Localization) then describes the configuration of individual programs for use with 8-bit character sets, together with the use of the international A4 paper size for printed output.

Currently, there are only a few freeware programs that use NLS. Not all UNIX systems support NLS in the C library, although both the POSIX standard and the ANSI-C standard define most of the functions presented here. Also, many