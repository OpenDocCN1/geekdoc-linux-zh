calling the run() method of a thread directly. Background execution can be accomplished only when start() is called – it invokes the thread-spawning logic and then proceeds to executing the payload.

Finally, change the client so that it sends some data to its master:

```
```
void ImagineReceiver::dataReady()
{
 ... 

QDataStream out(&block, QIODevice::WriteOnly);
out.setVersion(QDataStream::Qt_4_0);
out << QString("Hello, server!");
mySocket->write(block);
}
```
```

Multithreaded programs can show all kinds of odd behaviour due to a situation called race condition. If two runtimes access a shared element at the same time, havoc is guaranteed. Qt provides a variety of methods, such as mutexes, which can mitigate such problems.

# ## Advanced considerations

In the beginnings of the internet, every computer had its own public IP address. Nowadays many, if not most, systems find themselves behind layers of routers providing network address translation and/or firewall services.

The image on page 43 shows a network made up of two local networks connected to one another via the internet.

If a networked application on system A wants to connect to system B, router B must be configured to expose the port in question. This can usually be accomplished in the backend of the router – since every manufacturer provides a slightly different user interface, it’s best to refer to your router’s (online) manual.

# ## Conclusion

Well-versed developers can implement the most complex of protocols. Fortunately, Qt provides ready-made classes that implement commonly-used protocols such as HTTP. Next time, we will use one of these to create a small RSS reader.

# “Multithreaded programs can behave oddly”

```
```
void ImagineListenerClass::connectionIncoming()
{
	QTcpSocket *clientConnection = myServer->nextPendingConnection();
	connect(clientConnection, SIGNAL(disconnected()),
		clientConnection,
		SLOT(deleteLater()));

	QByteArray block;
	QDataStream out(&block, QIODevice::WriteOnly);
	out.setVersion(QDataStream::Qt_4_0);

	out << QString("Hello, client!");
	clientConnection->write(block);
	clientConnection->disconnectFromHost();
}
```
Fig 01
```

```
```
void ImagineReceiver::anConnected()
{
	qDebug() << "Connection successful";
}

void ImagineReceiver::errorOccurred(QAbstractSocket::SocketError anError)
{
	qDebug() << "Error: " << anError;
}
```
Fig 02
```

```
```
int main(int argc, char *argv[])
{
	QCoreApplication a(argc, argv);

	mySocket=new QTcpSocket();
	ImagineReceiver *myListener=new ImagineReceiver(mySocket);
	mySocket->connect(mySocket, SIGNAL(connec ted()), myListener, SLOT(anConnected()));
	mySocket->connect(mySocket, SIGNAL(readReady()), myListener, SLOT(dataReady()));
	mySocket->connect(mySocket, SIGNAL(error(QAbstractSocket::SocketError)),
			myListener, SLOT(errorOccurred(QAbstractSocket::SocketError)));
	mySocket->connectToHost(QHostAddress::LocalHost, 1825);
	return a.exec();
}
```
Fig 03
```

```
```
void ImagineListenerClass::connectionIncoming()
{
	QTcpSocket *clientConnection = myServer->nextPendingConnection();
	connect(clientConnection, SIGNAL(disconnected()), clientConnection,
		SLOT(deleteLater()));

	clientConnection->setParent(0);
	ImagineThread *myThread=new ImagineThread(clientConnection);
	connect(clientConnection, SIGNAL(readReady()), myThread, SLOT(dataReady()));
	myThread->start();

	QByteArray block;
	QDataStream out(&block, QIODevice::WriteOnly);
	out.setVersion(QDataStream::Qt_4_0);
	out << QString("Hello, client!");
	clientConnection->write(block);
}
```
Fig 04
```