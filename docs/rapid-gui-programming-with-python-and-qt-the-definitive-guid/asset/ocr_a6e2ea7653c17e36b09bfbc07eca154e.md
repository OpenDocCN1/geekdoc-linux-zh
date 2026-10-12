format, and Booleans. For character data such as the title and notes, we can include quotes, since only the meta-characters are not permitted.

```
```
def exportXml(self, fname):
    error = None
    fh = None
    try:
        fh = QFile(fname)
        if not fh.open(QIODevice.WriteOnly):
            raise IOError, unicode(fh.errorString())
        stream = QTextStream(fh)
        stream.setCodec(CODEC)
        stream << ('<"xml version=\'1.0\' encoding=\'%s\'>\n"
                "<!DOCTYPE MOVIES>\n"
                "<MOVIES VERSION=\'1.0\'>\n') % CODEC)
```
```

![](bbox=[0.03, 0.38, 0.1, 0.42])

We have chosen to use PyQt's QTextStream to write our XML file; we could just as easily have used the codecs module, although in that case we would need to convert the QStrings to unicodes.*

The method starts off in the now familiar way. Once the QTextStream has been created, we set its codec to UTF-8 as usual, and then we output the first three lines—these are always the same.

```
```for key, movie in self.__movies:
    stream << ("<MOVIE YEAR='%d' MINUTES='%d' "
            "ACQUIRED='%s'>\n") % (
        movie.year, movie.minutes,
        movie.acquired.toString(Qt.ISODate)))
    << "<TITLE>" << QString(movie.title) \
    << "</TITLE>\n<NOTES>"
    if not movie.notes.isEmpty():
        stream << "\n" << Qt.escape(
            encodedNewLines(movie.notes))
    stream << "\n</NOTES>\n</MOVIE>\n"
    stream << "</MOVIES>\n"```
```

We iterate over our movie data in the same way as we have done previously. The Qt.escape() function takes a QString and returns it with any XML meta-characters properly escaped. And we use our encodedNewLines() function to convert any paragraph and line breaks in the notes to their Unicode equivalents. We do not perform any escaping on the attributes because we know that they cannot contain any unacceptable characters. We have omitted the end of the method since the exception handling and return are structurally the same as those we have seen before.

> *PyQt 4.0 has a bug that prevents QTextStream from writing correctly, so for PyQt 4.0 we must use the codecs module. The problem does not exist in PyQt 4.1 and later versions.*