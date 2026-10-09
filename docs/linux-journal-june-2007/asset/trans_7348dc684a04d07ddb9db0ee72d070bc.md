

# 再次聆听你的思考！

![](img/526fd434dcfcf1b461b94c24ea170f36_58_0.png)

## WhisperStation™

### 酷炫... 极速... 静音！

- 适用于 64 位 HPC、游戏和图形设计应用
- 体验“寂静之声”。
- 致电我们的技术销售团队 508-746-7341，今天就设计您的专属 WhisperStation™。

WhisperStation™ 最初是为汽车行业中的一群功耗需求高、要求严格的工程师设计的。它集成了双核 AMD Opteron™ 或 Intel® EM64T™ 处理器、超静音风扇和电源，以及内部隔音材料，从而构建了一个强大且静音的计算平台。WhisperStation™ 标配 2 GB 高速内存、NVIDIA e-GeForce 或 Quadro PCI Express 图形适配器以及 20 英寸 LCD 显示器。可以根据您的确切硬件规格配置为任何 Linux 发行版。也可提供 RAID 选项。当用作 Microway 集群的主节点时，WhisperStation™ 也会让系统管理员感到非常满意！访问 www.microway.com 获取更多技术信息。

![](img/526fd434dcfcf1b461b94c24ea170f36_58_1.png)

![](img/526fd434dcfcf1b461b94c24ea170f36_58_2.png)

![](img/526fd434dcfcf1b461b94c24ea170f36_58_3.png)

# 使用 Qt 4.x 进行异步数据库访问

如何在 Qt 4 中编码以规避默认的同步数据库访问。

Dave Berton

Qt 4.x 中的数据库支持非常健壮。该库包含针对 Oracle、PostgreSQL、SQLite 以及许多其他关系型数据库的驱动程序。开箱即用的 Qt 数据库库还包含针对许多小部件的绑定，并为透明处理来自数据库的结果集提供了数据类型。但是，您的应用程序可能需要为这些便利性付出代价。所有数据库访问默认都是同步的，这意味着密集且耗时的 SQL 查询通常会锁定 UI，除非采取预防措施。使用服务器上的存储过程有时可以帮助缓解这种情况；然而，这并不总是可行或理想的。而且，通常应用程序生成的查询的长度和成本是无法预先得知的，这为不良的 UI 行为留下了隐患。人们不希望在奇怪的时刻应用程序“冻结”；然而，这是默认行为，因此我们必须与之抗争。

幸运的是，Qt 4.x 也提供了对多线程编程的健壮支持。通过将繁重的数据库工作放在单独的线程中，UI 可以自由地正常响应用户，而无需尴尬的中断。与所有并发编程一样，您必须采取预防措施以确保线程之间交互的正确顺序。例如，在线程之间共享数据时，使用互斥锁进行适当的保护。在线程之间通信时，仔细考虑交互的行为及其顺序。此外，当在使用与 UI 线程分离的线程内利用数据库连接时，您必须注意一些额外的注意事项。一种正确的实现，在考虑某些事项后，将显著提高数据库应用程序的 UI 行为和响应性。

## 线程策略

有几种方法可以将数据库负载分配到不同的执行线程中。幸运的是，在正确创建和使用数据库连接的细节上，它们都具有相同的特性。主要考虑因素是仅在使用该数据库连接创建的线程内使用它。对于常规的同步应用程序，默认行为是没问题的。`QSqlDatabase::addDatabase()` 静态函数在应用程序主 UI 线程的上下文中创建数据库连接。在此同一线程中执行的查询将导致阻塞行为。这是意料之中的。

为了在主 UI 线程并行运行查询，以便它们不会中断主事件处理循环，必须在该查询执行的线程中建立数据库连接，该线程应与主 UI 线程分离。无论您如何组织应用程序中的线程，您的设计必须能够在每个将执行数据库工作的线程上下文中建立连接。

例如，创建一个线程池，其中几个线程以轮询方式处理数据库查询负载（避免始终创建和销毁线程的开销），可以将耗时的工作推到主事件循环之外。或者，根据应用程序的需求，您可以简单地按需生成线程来执行数据库工作。在这两种情况下，您都必须为每个线程创建一个连接。

还有进一步的限制（由 Qt 使用的大多数底层特定数据库库施加）。一般规则是，连接不能被多个线程共享。这意味着您不能在启动时简单地创建连接池并按需将它们分配给各个线程。相反，每个线程必须在自己的上下文中建立并维护自己的连接。如果您违反这一点，可能会造成灾难性后果。可以使用 `QSqlDatabase::addDatabase()` 静态函数的名称参数在每个线程中建立多个独立连接，如列表 1 所示。

在列表 1 中，线程对象建立两个不同的数据库连接。每个连接都有单独的名称，以便 `QSqlDatabase` 可以在其内部列表中正确维护它们。最重要的是，每个连接都在每个对象的单独执行线程中建立——一旦新的执行线程启动，`run()` 方法就会由 `QThread::start()` 调用。`QSqlDatabase` 提供用于创建新连接的机制是线程安全的。列表 2 展示了另一种更通用方法的示例。

列表 2 中的伪代码创建并启动两个工作线程。每个线程建立到数据库的命名连接并等待工作。每个线程将始终只与其自己的数据库连接打交道，该连接永远不会被共享或在 worker 线程对象之外可见。

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

## 在线程间移动数据

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

