
```cpp
// Listing 1. Create two instances of QThread, one for queries, another for updates.

class QueryThread : public QThread
{
    public:
        QueryThread( QObject* parent = 0 )
        {
            //...
        }
        void run()
        {
            QSqlDatabase db = QSqlDatabase::addDatabase(
                "QPSQL", "querythread" );
            // use 'db' here
        }
};

class UpdateThread : public QThread
{
    public:
        UpdateThread( QObject* parent = 0 )
        {
            //...
        }
        void run()
        {
            QSqlDatabase db = QSqlDatabase::addDatabase(
                "QPSQL", "updatethread" );
            // use 'db' here
        }
};
```

```cpp
// Listing 2. A More Generic Approach with a Single Instance of QThread Used Twice

class QueryThread : public QThread
{
    public:
        QueryThread( const QString name )
            : m_connectionName(name)
        {
            //...
        }
        void run()
        {
            QSqlDatabase db = QSqlDatabase::addDatabase("QPSQL", m_connectionName );
            //...
            db.open();
            forever
            {
                // wait for work
                // and then execute it...
            }
        }
    }

    void main()
    {
        QApplication app(...);
        MainWindow mw;
        QueryThread db1("queries");
        db1.start();
        QueryThread db2("updates");
        db2.start();
        //...
        mw.show();
        app.exec();
    }
```

设置线程特定的连接并在线程内运行查询只是问题的一部分。需要决定数据如何在工作线程和主应用程序 UI 线程之间来回传递。额外方法将向线程对象提供数据库工作以执行，而这些方法本身需要是线程安全的。

`QCoreApplication` 以线程安全的方式将这些事件从应用程序线程传递给工作线程，它们将由工作线程在其自己的执行上下文中处理。这一点至关重要，因为工作线程将仅在其自己的上下文中使用其数据库连接（列表 3）。这种方法在另一个方向上同样有效。由单独工作线程发布的事件将回到主 UI 事件循环中以便处理，处于 UI 执行线程的上下文中。这些事件可以例如包含查询或数据库更新的结果。这种方法很方便，因为工作线程可以简单地“发布并忘掉”，Qt 将为您处理线程间通信、互斥和内存管理。构建这种类型系统所需的所有必要事件和事件处理器具有优势——最显著的是编译时类型。

# 在线程间移动数据

您应该遵守围绕不同执行线程间共享数据的所有通常注意事项，包括互斥锁和等待条件的正确使用。此外，关于数据大小还有一个额外的复杂因素，在从数据库返回结果集的情况下，数据量可能非常大。

Qt 提供了几种专门的机制在线程之间发送数据。您可以使用线程安全函数 `QCoreApplication::postEvent()` 手动向任何线程中的任何对象发布事件。事件将由创建目标对象的线程的事件循环自动分发。为了在每个线程中创建事件循环，使用 `QThread::exec()`。使用这种方法，线程被赋予以事件形式执行的“工作”。

现在，线程间的通信变成了一件事：将一个线程的信号连接到另一个线程的槽，Qt 将处理线程间交换数据的互斥和线程安全问题。

```cpp
// Listing 3. Code That Shares Information from Worker Thread to Application Thread via Event

class WorkEvent : public QEvent
{
    public:
    enum { Type = User + 1 }
    WorkEvent( const QString& query )
      : QEvent(Type)
      , m_query(query)
    {}

    QString query() const
    {
      return m_query;
    }

  private:
    QString m_query;
};

QueryThread thread;
thread.start();
// ...
WorkEvent* e = new WorkEvent("select salary from employee where name='maggelena';");
app.postEvent( &thread, e );
// ...
```

```cpp
// Listing 4. Sharing information across threads is cleaner with signals and slots.

class Worker; // forward decl
class QueryThread : public QThread
{
 QueryThread();
 signals:
  void queryFinished( const QList<QSqlRecord>& records );
 slots:
  void slotExecQuery( const QString& query );
 signals:
  void queue( const QString& query );
 private:
  Worker* m_worker;
};

int main()
{
  QApplication app;

  MainWin mw;

  QueryThread t;
  t.start();

  connect(&mw, SIGNAL( execQuery(const QString&)),
          &t, SLOT( slotExecQuery(const QString&)));

  connect(&t, SIGNAL( queryFinished(const QList<QSqlRecord>&)),
          &mw, SLOT( slotDisplayResults(const QList<QSqlRecord>&)));

  mw.show();
  return app.exec();
}
```

# 特性：使用 Qt 4.x 实现异步数据库访问

检查。然而，设计并妥善处理所有事件可能是一项艰巨的任务，尤其是当你的应用程序需要执行多种类型的数据库查询，具有多种返回类型，每种类型都需要关联的事件和事件处理器时，情况更是如此。

幸运的是，Qt 允许在不同线程之间连接信号和槽——只要这些线程正在运行它们自己的事件循环。与发送和接收事件相比，这是一种更简洁的通信方法，因为它避免了在任何非平凡应用程序中变得必要的簿记工作和中间 `QEvent` 派生类。线程间的通信现在变成了将一个线程的信号连接到另一个线程的槽，而线程间交换数据时的静默和线程安全问题由 Qt 处理。
