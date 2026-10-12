
## findtr UTILITY

```cpp
HiLabel:HiLabel( QWidget *p, const char *n )
: QLabel( p, n )
{
// Hard-coded default string, translated text
setText( tr( "Hello World" ) );
}
int
main( int argc, char **argv )
{
QApplication *app = new QApplication( argc, argv );
// Create a new translator
QTranslator xlat = QTranslator( 0 );
// Load the Spanish translation
xlat.load( "hello_sp.qm", "." );
// Install the new translator
app->installTranslator( xlat );
// Create a translated label
HiLabel *l = new HiLabel();
app->setMainWidget( l );
return( app->exec() );
}
```

The above call to QObject::tr() is where the actual translation takes place. A translation table file that contains an appropriate translation from our U.S. English example is still required and will be loaded at runtime by the QTranslator instance created in main(). Three utilities are provided by Qt to assist in creating the translation table files. These are findtr, msg2qm, and merger. The .po translation files can be created by hand, but it's much easier to use the utilities. Each is discussed below.

The findtr program (actually a Perl script) can locate all calls to tr( const char * ) within the named input files and will generate a text table that can be hand-edited to include the string translations. Typically, you will create a single translation file using a syntax something like:

```bash
findtr hello.cpp > hello_sp.po
```

This creates a baseline translation file that can be copied to sensibly-named files for each of the target languages (e.g., hello_sp.po for a Spanish file). Using the hello program above, findtr will generate some header information which helps to identify the translation file and the version of the *findtr* utility that was used to generate it. It will also generate the following entry:

```text
#: hello.cpp:15
msgid "HiLabel::Hello World"
msgstr ""
```

The actual table entries are made up of a *msgid* and *msgstr* pair. You can easily identify the required translation from the *msgid* value, but don't translate the entire text of the *msgid* value, as the scoping information (required by the *QApplication::translate()* method) is included. Assuming our target language is Spanish, the following fragment of *hello_sp.po* is a hand-edited Spanish translation for the example:

```text
#: hello.cpp:15
msgid "HiLabel::Hello World"
msgstr "Hola Mundo"
```

We are now ready to create the platform-independent binary message file with the *msg2qm* utility.

## msg2qm UTILITY

Once you have used the *findtr* utility to create the baseline translation table and completed the task of translating all the strings, you are ready to create the platform-independent Qt message files for the target languages. This is done using the *msg2qm* utility that can be found under the *src/util* directory in the Qt distribution. For some bizarre reason, the default Qt build process will compile the *findtr* utility (which you don't need) and install it in the *bin* directory of the Qt distribution—but the *msg2qm* (which you *do* need) and *merger* utilities must be explicitly compiled from their *source* directory, *src/util*.

To create the Spanish message file for the preceding example, simply execute the utility as follows:

```bash
msg2qm hello_sp.po hello_sp.qm
```

The *msg2qm* utility converts the human readable translation file into an internal format that can be read more quickly. When you execute the example program, it will now display in Spanish.

## merger UTILITY

As you make changes or additions to your application, you will probably need to change your translation files accordingly. To do so, you can simply run the *findtr* utility again to create a new baseline translation file, then use the *merger* utility to merge the changes into your existing language-specific translation files. This will recreate the target translation file with comments about the changes.

Once you've edited the new translation files, you can use the *msg2qm* utility to create the Qt message files that QtTranslator expects.

```bash
findtr hello.cpp > hello.po # create a new base
```

(Edit hello.po, making any required changes or additions.)

```bash
merger hello.po hello_sp.po
msg2qm hello_sp.po hello_sp.qm
```

It's a good idea to maintain the translation files with a good version control system such as RCS, Microsoft VSS, or whatever you prefer. This is especially true during the initial implementation, when the project is subject to major feature changes. It is very easy to lose track of which translation files are appropriate for a given release of the application.

## INPUT METHODS

Of course, Qt doesn't address *all* the complex issues involved in internationalized application development. The underlying window system must take responsibility for much of the low-level functionality. This is especially true in the case of keyboard input methods. Very few companies have the resources that are required to provide a comprehensive set of input methods, but because Qt is so widely accepted by the Linux community, there are an ever-increasing number of freely available implementations.

Those languages with unidirectional single-byte encodings (European Latin 1 and KOI8-R etc.) and the unidirectional multibyte encodings (East Asian EUC-JP, EUC-KR, etc.) are directly supported. Support for “complex” encodings—those that may require right-to-left input or complex character composition (e.g., Arabic, Hebrew, and Thai script)—will *probably* be implemented in a later release.

The following list is the (more or less) current state of encodings support (assuming your OS doesn't provide the support already, as is the case with Linux):

- Microsoft Windows—The local encoding is always supported.
- ISO standard encodings—ISO 8859-1, ISO 8859-2, ISO 8859-3, ISO 8859-4, ISO 8859-5, ISO 8859-7, ISO 8859-9, and ISO 8859-15 are fully supported.
- Arabic (ISO 8859-6-1) and Hebrew (ISO 8859-8-1) encodings are not supported, but are under development by third parties.
- KOI8-R is fully supported.
- EUC-JP is fully supported.
- EUC-KR is fully supported (thanks to Mizzi Research, Inc.).
- Big5—Qt contains a Big5 codec developed by Ming Che-Chuang. Testing is under way with the xcin (2.5.x) XIM server.
- “Simplified” Chinese—currently unsupported.
- EUC-TW—Under external development.

You should have no trouble working with the proprietary input methods such as those provided with HP/UX locale packages, unless you require the functionality of XIM protocol revision 4.0, as HP still provides version 3.5.

Qt makes it much easier to code internationalization support into any application— even existing Qt projects that weren’t originally coded “properly.” Having added language translation support to an existing medium-scale project (there is virtually no input other than via mouse), I learned an important lesson: Add language translation support (at least) whether the specification calls for it or not. It’s easy; there is no noticeable performance hit, and you just might save yourself a few hours of future time, because you never know when you’ve told your project is going to ship to a foreign country.

At the cost of “plugging” my employer’s products, I think it’s worth noting that Hewlett-Packard and most other large UNIX vendors market PS/2 keyboards (with mini-DIN connectors) that sport language-specific keycaps. At the expense of plugging a competitor’s products, IBM sells PS/2 keyboards with detachable keycap sets for various languages. These will work on most Intel-based Linux implementations, although you will still need to provide some form of input method, or maybe just a custom keyboard configuration for your X server. Contact your favorite vendor for pricing on specialized keyboards, but don’t expect a lot of vendor support for that keyboard on Linux.

## PLATFORM-INDEPENDENT PROJECTS

There are several schools of thought regarding the creation and maintenance of project build scripts. On Linux (or other UNIX-like) platforms, developers are already comfortable with the Makefile format. These Makefiles are often created on demand by a configure script that is either a highly customized shell, Perl, or Tcl script, or the product of a GNU autotools script. Developers from Microsoft Windows platforms are usually more comfortable with a Visual C++ project or workspace file. This creates yet another platform-dependency barrier that is separate from other platform dependencies.
