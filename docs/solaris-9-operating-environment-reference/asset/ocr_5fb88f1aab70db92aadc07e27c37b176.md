# Description

ipcm removes one or more messages, semaphores, or shared memory identifiers.
If you specify either the -C or -N flag, the real and effective UID/GID is set to the real
UID/GID of the user invoking ipcs.

# Options

+   -m shmid Remove the shared memory identifier shmid from the system. Destroy the shared memory segment and data structure associated with it after the last detach.
-q msgid Remove the message queue identifier msgid from the system, and destroy the message queue and data structure associated with it.
-s semid Remove the semaphore identifier semid from the system, and destroy the set of semaphores and data structure associated with it.
-M shmkey Remove the shared memory identifier, created with key shmkey, from the system. Destroy the shared memory segment and data structure associated with it after the last detach.
-Q msgkey Remove the message queue identifier, created with key msgkey, from the system, and destroy the message queue and data structure associated with it.
-S semkey Remove the semaphore identifier, created with key semkey, from the system, and destroy the set of semaphores and data structure associated with it.

The details of the removals are described in msgctl(2), shmctl(2), and semctl(2).
Use the ipcs command to find the identifiers and keys.

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNWpc |

# See Also

ipcs(1), msgctl(2), msgget(2), msgrcv(2), msgsnd(2), semctl(2),
semget(2), semop(2), shmctl(2), shmget(2), shmat(2), attributes(5)

# ipcs — Report Interprocess Communication Facilities Status

# Synopsis

```
/usr/bin/ipcs [-aBcimopqst] [-D mtype]
```