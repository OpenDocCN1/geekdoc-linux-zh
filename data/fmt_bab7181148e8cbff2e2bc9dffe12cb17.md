
```cpp
// Log.cpp

#include <Log.h>
#include <qdatetime.h>
#include <qfile.h>
#ifdef WIN32
#include <io.h>
#endif
#include <ctypes.h>

// Ctor: filename, max size, redirect stdout/stderr
Log::Log( const QString &file, int size, bool stredir )
{
    doseq = true;
    redir = stredir;
    limit = size;
    opensuccess = false;
    seq = 0L;
    if(strcmp(file, "stderr") ) {
        _create( file, size, stredir );
    } else {
        ofp = new QFile();
        ofp->open( IO_WriteOnly, stderr );
        opensuccess = true;
    }
}

// Create file method, rotate log files
void
Log::create( const QString &file, int size, bool stredir )
{
    if(file != 0) {
        fname = file;
        ofp = new QFile( file );
    } else {
        ofp = new QFile();
        ofp->open( IO_WriteOnly, stderr );
        if(stredir == true) {
            opensuccess = true;
#ifdef WIN32
            dup2(ofp->handle(), 1);
#else
            _dup2(ofp->handle(), 1);
#endif
        }
    }
    return;

    if(ofp->size() >= limit) {
        QString nn;
        nn.sprintf("%s.old", file);

#ifdef WIN32
        link(file, nn);
        unlink(file);
#else
        rename( file, nn );
#endif

        if( ofp->open( IO_WriteOnly|IO_Truncate ) == false) {
            opensuccess = false;
            delete ofp;
            ofp = new QFile();
            ofp->open( IO_WriteOnly, stderr );
        } else {
            opensuccess = true;
        }
        if(stdredir == true) {
#ifdef WIN32
            _dup2(ofp->handle(), 1);
            _dup2(ofp->handle(), 2);
#else
            dup2(ofp->handle(), 1);
            dup2(ofp->handle(), 2);
#endif
        }
    } else {
        if(ofp->open( IO_WriteOnly|IO_Append ) == false) {
            opensuccess = false;
            delete ofp;
            ofp = new QFile();
            ofp->open( IO_WriteOnly, stderr );
        } else {
            opensuccess = true;
        }
        if(stdredir == true) {
#ifdef WIN32
            _dup2(ofp->handle(), 1);
            _dup2(ofp->handle(), 2);
#else
            dup2(ofp->handle(), 1);
            dup2(ofp->handle(), 2);
#endif
        }
    }
}

Log::~Log()
{
    ofp->flush();
    ofp->close();
}

void
Log::raw(const char *fmt, ...)
{
    char p[4096];
    va_list ap;

    if(ofp == 0) return;

    va_start(ap, fmt);
#ifdef _HPUX_SOURCE
    vsprintf(p, fmt, ap);
#endif
#ifdef WIN32
    vsprintf(p, fmt, ap);
#endif
#ifdef LINUX
    vsnprintf(p, 4095, fmt, ap);
    va_end(ap);
#endif

    ofp->writeBlock(p, strlen(p));

    if(ofp->size() >= limit && ofp->handle() != fileno(stderr)) {
        ofp->flush();
        ofp->close();
        create(fname, limit, redir);
    }
}

void
Log::print(const char *fmt, ...)
{
    char p[4096];
    QString buf;
    va_list ap;

    if(ofp == 0) return;
    memset(p, 0, 4096);

    va_start(ap, fmt);
#ifdef _HPUX_SOURCE
    vsprintf(p, fmt, ap);
#endif
#ifdef WIN32
    vsprintf(p, fmt, ap);
#endif
#ifdef LINUX
    vsnprintf(p, 4095, fmt, ap);
    va_end(ap);
#endif

    QDateTime t = QDateTime::currentDateTime();
    if(doSeq == true) {
        buf.sprintf("%06ld %02d:%02d:%02d.%03ld %02d/%02d: %s",
                    seq++,
                    t.time().hour(),
                    t.time().minute(),
                    t.time().second(),
                    t.time().msec(),
                    t.date().month(),
                    t.date().day(), p );

    } else {
        buf.sprintf("%02d:%02d:%02d.%03ld %02d/%02d: %s",
                    t.time().hour(),
                    t.time().minute(),
                    t.time().second(),
                    t.time().msec(),
                    t.date().month(),
                    t.date().day(), p );

    }

    ofp->writeBlock(buf, strlen(buf));

    if(ofp != 0 && ofp->size() >= limit &&
       ofp->handle() != fileno(stderr)) {
        ofp->flush();
        ofp->close();
        strcpy(p, fname);
        create(const_cast<char*>(p), limit, redir);
    }
}

void
Log::lprint(const char *file, int line, const char *fmt, ...)
{
    char p[4096];
    QString buf;
    va_list ap;

    if(ofp == NULL) return;
    memset(p, 0, 4096);

    va_start(ap, fmt);
#ifdef _HPUX_SOURCE
    vsprintf(p, fmt, ap);
#endif
#ifdef WIN32
    vsprintf(p, fmt, ap);
#endif
#ifdef LINUX
    vsnprintf(p, 4095, fmt, ap);
#endif

    QDateTime t = QDateTime::currentDateTime();
    if(doseq == true) {
        buf.sprintf("%06ld %02d:%02d:%02d.%03ld ",
```

## 日志输出格式与缓冲区转储

以下代码片段展示了日志时间戳格式的字符串拼接及缓冲区转储（`buf_dump`）功能的实现逻辑：

```cpp
```
