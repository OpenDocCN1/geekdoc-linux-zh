
## Example 8.1. Polling Read Example

```c
/*************************************************************/
/** Polling Read Example: reading an audio stream, ***/
/** processing the data, and playing it. ***/
/*************************************************************/
...
if ( fcntl( sd, F_SETFL, O_NONBLOCK ) != 0 )
    perror("fcntl--could not set nonblocking");
...
done = 0;
while ( !done )
{
    int bytes;
    Queue ProcessingQueue;
    Queue OutputQueue;
    /**** Get any pending data ****/
    if ( (bytes = recv( sd, buffer, sizeof( buffer ), 0 )) > 0 )
        QueueData( ProcessingQueue, buffer);
    /**** Convert a certain number of bytes from the ****/
    /**** processing queue--typically faster than recv() ****/
    ConvertAudio( ProcessingQueue, OutputQueue);
    if ( /*** output queue is far enough ahead **/ )
        PlayAudio( OutputQueue );
    /**** If data stream is done & output queue empty... ****/
    if ( bytes == 0 && /***--output queue empty---*/ )
        done = 1;
}
...
```

This example accepts data, enqueues it, and processes it. However, it does have a problem: If there is no data in either queue, the `while` statement becomes a tight loop. To solve this problem, you could insert a delay, since audio is a real-time issue.

### Polling Writer

The program runs several times faster than any I/O function. (In fact, to improve the performance of your computer, get more memory and replace old, slow I/O. Just getting a faster CPU is not as effective.) So, when your program transmits a message or makes any request, the operating system puts your program on hold for quite a while.

The polling writer has a similar algorithm to the polling reader. It's a good idea to couple data generation and processing with the transmitter. The preparation is the same: Use the `fcntl()` system call with the same parameters.

The problem you may have to deal with in a polling writer is the exact opposite from the reader. The reader may have no data to work with, thus placing the reader into a tight loop. The writer can generate data more quickly than `send()` can transmit it (*writer pileup*).

For instance, consider the algorithm in *Listing 8.2* to send photos from a digital camera to a few clients.

## Example 8.2. Polling Writer Example

```c
/*************************************************************/
/** Polling Writer Example: sending an image to several ***/
/*** clients. ***/
/*************************************************************/
...
int pos[MAXCLIENTS];
zero( pos, sizeof( pos) );
for ( i = 0; i < ClientCount; i++ )
if ( fcntl(client[i], F_SETFL, O_NONBLOCK) != 0 )
perror( "Fcntl--could not set_nonblocking" );
...
done = 0;
/*--- repeat until all the clients get the whole message ---*/
while ( !done )
{
int bytes;
done = 1;
/*--- For all clients... ---*/
for ( i = 0; i < ClientCount; i++ )
/*--- If still more to send to client... ---*/
if ( pos[i] < size )
{
/*--- send msg, tracking how many bytes sent ---*/
bytes = send(client[i], buffer+pos[i],
size-pos[i], 0 );
if ( bytes > 0 )
{
pos[i] += bytes;
/*--- if all the clients are done, exit ---*/
if ( pos[i] < size )
done = 0;
}
}
}
...
```

In this code, the clients have to be tracked individually, because they may be accepting data at different rates. The pos integer array tracks byte position in a buffer where each client is processing. You could expand this algorithm to encompass timeouts.

Another problem may be that your server may get another image while the first is still being sent out, causing writer pileup. To solve this problem, choose one of these options:

- Append the new message onto the old.
- Cancel the last message and begin to send the new one.
- Change the camera's frame rate.

In all cases, base your choice of options on how critical the data is, how much could be lost, and how variable the connections are. See Chapter 4, "Sending Messages Between Peers," for a list of guidelines.

## Polling Connections

A more rare polling algorithm involves connecting clients from different ports. The server waits for a client to connect, and typically, the server program offers only one port. While this is customary, you can have as many ports open as you want within a program. However, designers think of a program as having a specific purpose and a port as providing a specific service.

Some port services are so fundamental and trivial that writing programs for each is a waste of time, effort, and memory. But a socket may connect to only one port. Instead, consider writing a polling socket program, as shown here:

```c
/*******************************************/
/*** Polling Connection Example: check various ports for ***/
/*** connections creating a new task to answer each ***/
/*** request. ***/
/*******************************************/
"";
/* --- Set nonblocking for each socket --- */
for ( i = 0; i < numports; i++ )
    if ( fcntl(sd[i], F_SETFL, O_NONBLOCK) != 0 )
        perror("Fcntl--can't set nonblocking on port#%d", i);

for (;;) /* Do this forever */
{
    int client;
    for ( i = 0; i < numports; i++ )
        if ( (client = accept(sd[i], &addr, &size)) > 0 )
            SpawnServer(sd[i], i);

    /**** Do housekeeping ****/
}
"";
```

This may seem like a great idea, but creating a separate task for each `accept()` may be more manageable. In fact, the best solution is to use the `select()` system call, which waits for a number of I/O channels to unblock (refer to Chapter 7, "Dividing the Load: Multitasking," for more information on `select()`).

### Asynchronous I/O

Getting the operating system to tell you when a channel is ready for more I/O requests turns around the problem of file I/O in your favor. This affords more time for the program to spend on computation and less time stalled in various system calls.

An asynchronous read is similar to the blinking light on an office phone indicating voicemail. In the same vein, the telephone callback feature is like the asynchronous write. Picture asynchronous I/O as a notification of channel availability.

The system implements this asynchronous I/O with the `SIGIO` signal (sometimes called *signal-driven I/O*). Programs get a `SIGIO` when data is ready for reading or when a write channel is ready for more data. As with all signals, you know nothing more than a signal occurred. So, in the case of a program getting an `SIGIO` when two channels are open, it is not readily apparent which channel to check.

Exceptions present another problem. The kernel does not issue a signal if an error occurs on the channel. It's not readily apparent when a program loses connection with the client, unless you actually test the channel in the program.

The program begins the signal-driven I/O by instructing the kernel to accept a `SIGIO` signal. When the signal arrives, the signal handler sets a flag that the main program watches. The main program loop in turn begins processing, occasionally checking the flag that indicates the signal arrived. The handler may do the I/O processing itself and then flag the main loop, or it could just leave the I/O for the main loop.

How does this differ from polling? Both algorithms need to check periodically if the I/O channel is ready. Polling calls don't block the system calls but do require periodic checking. Similarly, the main loop has to poll on the flag being set by the signal-driven I/O.

The primary difference is how much time the program spends in the system calls. The signal-driven I/O spends very little time in the `send()` and `recv()` system calls: the kernel tells your program when it is ready. On the other hand, polling has to repeatedly make system calls.

The algorithm in Listing 8.3 provides a general idea how the process works.

## Example 8.3. Signal-Driven I/O Algorithm

```c
/*******************************************/
/*** General Asynchronous or Signal-Driven I/O Algorithm ***/
/*******************************************/
int ready=0;
...
void sig_io(int sig)
{
    /**** IF RECV(): Get all pending data ****/
    /**** IF SEND(): Send all processed data ****/
    ready = 1;    /* tell main loop: "transaction complete" */
}
for (; ;)
{
    if ( ready > 0 )
    {
        /**** Block SIGIO temporarily ****/
        ready = 0;
        /**** IF RECV(): copy data into processing area ****/
        /**** IF SEND(): fill output buffer from ****/
        /**** ~processed data queue ****/
        /**** Unblock SIGIO ****/
    }
    /**** Process incoming data ****/
    /**** --OR- ****/
    /**** Generate more data to send ****/
}
...
```

Blocking a SIGIO signal may appear to be a little unusual. Because the signal handler and the main loop share the same variables, you have a critical section (see the section "Mutual Exclusion (Mutex)" in Chapter 7). Turning off the signal handler is an important mutual exclusion device (mutex).

### NOTE

### Queued Messages

To get all the pending messages, you may have to call the `send()` and `recv()` calls several times in the handler. The kernel may issue several signals at once to your program, but your program gets only one signal type at a time. If two identical signals arrive very closely together, your program gets only one.

You start the SIGIO messages using the `fcntl()` system call. This system call not only tells the kernel to make the socket descriptor asynchronous (remember that this applies to all file descriptors) but also tells the kernel to direct the signals to a specific process. For example, the following code segment turns on the SIGIO signals and directs them to the current task:

```c
/*******************************************/
```
