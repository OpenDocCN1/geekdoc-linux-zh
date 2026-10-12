
```cpp
int main(int argc, char *argv[])
{
    fstream NamedPipe;
    ifstream Fin;
    string InputFile;
    string Word;
    int N;
    strstream VirtualPage;

    NamedPipe.open("Channel-one",ios::in | ios::out);
    if(NamedPipe.bad()){
        cerr << "Could not open Channel-one" << endl;
    }
    for (N=1; N<argc; N++)
        SS.insert(argv[N]);
    do{
        getline(NamedPipe,InputFile);
        Fin.open(InputFile.c_str());
        if(!Fin.is_open())
            cerr << "Could not open " << InputFile << endl;
        while(Fin.good()){
            Fin >> Word;
            if(!Fin.fail())
                Contents.insert(Word);
        }
        Fin.close();
        if(includes(Contents.begin(),Contents.end(),SS.begin(),SS.end()))
            VirtualPage << "Located In " << InputFile << endl;
        Contents.erase(Contents.begin(),Contents.end());
    } while(InputFile != "done");
    NamedPipe.close();
```

```cpp
unlink("Channel-one");
VirtualPage << ends;
KApplication TextSearch(argc,argv);
KMsgBox("SearchResults",
SearchResults = new KMsgBox(NULL,"Multithreaded Search",
VirtualPage.str(),
MsgBox::EXCLAMATION,
"Task B is Complete");
TextSearch.connect(&TextSearch,SIGNAL(lastWindowClosed()),
SLOT(quit()));
TextSearch.setMainWidget(SearchResults);
SearchResults->show();
return(TextSearch.exec());
```

编译：

```bash
c++ -o mt_search_dir mt_search_dir.cpp -lpthread
```

以及：

```bash
c++ -o mt_find_string -I $KEDIR/include -I $QTDIR/include
mt_find_string.cpp -L $KEDIR/lib
-L $QTDIR/lib -lqt -lkdecore -lkdeui
```

如果你使用了线程安全的库，请在编译行中包含 `-D_REENTANT`。运行程序，请输入：

```bash
./mt_search_dir SearchText
```

## 面向对象的并发方法

在第 9 章中，我们建议你将应用程序划分为框架（framework）和集合（ensemble）。在这里，我们建议将并发局部化在应用程序类内部。也就是说，尽量减少跨框架和集合共享的临界区数量。如果可能，设计你的类，使得只有类方法可以访问类内部的临界区。使用适当的同步变量保护每个类的临界区。这些同步变量应该是类的成员。

## 第 15 章 * 编写可以多任务的应用程序 499

面向对象的并发方法是为 Linux 应用程序添加并发特性的最简单、最安全的方法之一。这种方法需要一组同步类。虽然 Linux 线程不是一个类库，但很容易从线程函数和数据类型构建接口类。

## 列表 15-5: 一个包含 safe_container 类定义的程序

```cpp
// 列表 15-5
// safe_container 类的定 义
#include "mutex.h"

template<class container,class object>
class safe_container {
protected:
    container C;
    mutex Mtx;
public:
    void addRear(object Obj);
    object removeFront(void);
    int empty(void);
};

template<class container,class object>
void safe_container<container,object>::addRear(object Obj)
{
    Mtx.lock();
    C.push_back(Obj);
    Mtx.unlock();
}

template<class container,class object>
object safe_container<container,object>::removeFront(void)
{
    object Temp;
    Mtx.lock();
    if(!C.empty()){
        Temp = C.front();
        C.pop_front();
    }
    Mtx.unlock();
    return(Temp);
}

template<class container,class object>
int safe_container<container,object>::empty(void)
{
    int X;
    Mtx.lock();
    if(C.empty()){
        X = 1;
    }
    else{
      X = 0;
    }
    Mtx.unlock();
    return(X);
}
```

每当调用访问 `safe_container` 数据组件的方法时，都会使用 `safe_container` 类中的互斥锁组件。互斥锁组件是一个接口类。列表 15-6 显示了 `mutex` 类的定义。

## 列表 15-6: 简单互斥锁接口类的定义

```cpp
// 列表 15-6
// 简单互斥锁接口类的定义

#include "thread.h"

class mutex{
protected:
  pthread_mutex_t Mutex;
  pthread_mutexattr_t Attr;

public:
  mutex(void);
  ~mutex(void);
  mutex(pthread_mutexattr_t Attr);
  void lock(void);
  void unlock(void);
};

mutex::mutex(void)
{
  pthread_mutexattr_init(&Attr);
  pthread_mutex_init(&Mutex, &Attr);
}

mutex::mutex(pthread_mutexattr_t Attr)
{
  Attr = Attr;
  pthread_mutexattr_init(&Attr);
  pthread_mutex_init(&Mutex, &Attr);
}

mutex::~mutex(void)
{
  pthread_mutexattr_destroy(&Attrib);
  pthread_mutex_destroy(&Mutex);
}
void mutex::lock(void)
{
  pthread_mutex_lock(&Mutex);
}
void mutex::unlock(void)
{
  pthread_mutex_unlock(&Mutex);
}
```

`mutex` 类和 `safe_container` 类允许我们为文本搜索应用程序添加并发性。

要编译该应用程序，`KDEDIR` 应该指向包含 KDE 头文件和库文件的目录。`QTDIR` 应该指向包含 Qt 头文件和库文件的目录。你需要 `safe_container.cpp`、`mt_search_dir2.cpp`、`mutex.h`、`mutex.cpp` 和 `mt_find_string.cpp` 文件。这些文件包含在随带的 CD 光盘的 `listings` 目录中。编译命令如下：

```bash
c++ -o mt_thread_app mt_search_dir2.cpp mutex.cpp -lpthread
```

以及
