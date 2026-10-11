
The example programs used in this chapter will use only a cmsg_level value of SOL_SOCKET. The control message types that are of interest to you in this chapter are shown in Table 17.4.

Table 17.4: cmsg_type Types for cmsg_level=SOL_SOCKET

| cmsg_level | Description |
| --- | --- |
| SCM_RIGHTS | The ancillary data object is a file descriptor. |
| SCM_CREDENTIALS | The ancillary data object is a structure containing credential information. |

## Introducing the cmsghdr(3) Macros

Due to the complexity of structuring the ancillary data, a number of C macros were provided to make this easier for you. Additionally, these macros enable much greater portability between different UNIX platforms and provide some insulation against changes that might occur in the future. These macros are described by the man page cmsghdr(3) and the synopsis for them are as follows:

```c
#include <sys/socket.h>
struct cmsghdr *CMSG_FIRSTHDR(struct msghdr *msg);
struct cmsghdr *CMSG_NXTHDR(struct msghdr *msg, struct cmsghdr *cmsghdr);
size_t CMSG_ALIGN(size_t length);
size_t CMSG_SPACE(size_t length);
size_t CMSG_LEN(size_t length);
void *CMSG_DATA(struct cmsghdr *cmsghdr);
```

> **TIP**
>
> Some of the macros presented in this chapter are not available on other UNIX platforms. For example, FreeBSD UNIX lacks the CMSG_ALIGN(), CMSG_SPACE(), and CMSG_LEN() macros. This should be borne in mind if you are writing code that must compile on other UNIX platforms in addition to Linux.

## The CMSG_LEN() Macro

This macro accepts as an input parameter the size of the object that you want to place into the ancillary data buffer. If you review Figure 17.1, you see that this macro computes the byte length of the cmsghdr header structure plus any pad characters that might be required, added to the length of the data object. This value is used to set the cmsg_len member of the cmsghdr object.

The following example shows how you would compute the value for the cmsg_len member, if the ancillary object is a file descriptor (this example just prints the value):

```c
int fd; /* File descriptor */
printf("cmsg_len = %d\n", CMSG_LEN(sizeof fd));
```

## The CMSG_SPACE() Macro

This macro is used to compute the total space required for the ancillary data object and its header. Although the CMSG_LEN() macro computes a similar length, the CMSG_LEN() value does not include possible trailing pad bytes (refer to Figure 17.1). The CMSG_SPACE() macro is useful for determining the buffer size requirements, as shown in the following example:

```c
int fd; /* File descriptor */
char abuf[CMSG_SPACE(sizeof fd)];
```

This example declares enough buffer space in abuf[] to hold the header, pad bytes, the ancillary data object itself, and any final pad bytes. If multiple ancillary data objects are being constructed in the buffer, be sure to add multiple CMSG_SPACE() macro calls together to arrive at the total space required.

## The CMSG_DATA() Macro

This macro accepts a pointer to the cmsghdr structure. The pointer value returned points to the first byte of ancillary data that follows the header and pad bytes, if any. If the pointer mptr points to a valid ancillary data message header that describes a file descriptor, the file descriptor can be extracted with the following example code:

```c
struct cmsghdr *mptr;
int fd; /* File descriptor */
fd = *(int *)CMSG_DATA(mptr);
```

## The CMSG_ALIGN() Macro

This is a Linux extension macro that is not part of the Posix.1g standard. Given a byte length as input, this macro computes a new length, which includes any additional pad bytes that are required to maintain alignment.

## The CMSG_FIRSTHDR() Macro

This macro is used to return a struct cmsghdr pointer to the first ancillary object within the ancillary data buffer. The input value is the pointer to the struct msghdr structure (do not confuse this with the struct cmsghdr). This macro evaluates the msghdr members msg_control and msg_controllen to determine whether any ancillary objects exist in the buffer. Then, it computes the pointer to be returned.

The pointer value returned is a NULL pointer if there are no ancillary data objects present. Otherwise, the pointer points to the first struct cmsghdr present. This macro is used at the start of a for loop, to start iterating through the ancillary data objects present.

## The CMSG_NEXTHDR() Macro

This macro is used to return the struct cmsghdr pointer of the next ancillary data object. This macro accepts two input arguments:

- The pointer to the struct msghdr structure
- The pointer to the current struct cmsghdr

This macro returns a NULL pointer if there is no next ancillary data object.

## Iterating Through Ancillary Data

When ancillary data is received, the CMSG_FIRSTHDR() and CMSG_NEXTHDR() macros are used to iterate through the ancillary data objects. The following example code shows the general form that the for loop and macros should take:

![](img/961a0296fe36074690a9847b79332eff_456_0.png)

```c
struct msghdr mshg;         /* Message hdr */
struct cmsghdr *cmshg;      /* Ptr to ancillary hdr */
int *fd_ptr;                /* Ptr to file descript.*/
int received_fd;            /* The file descriptor */

for ( cmsg=CMSG_FIRSTHDR(&mshg); cmsg!=NULL; cmsg=CMSG_NEXTHDR(&mshg,cmshg) ) {
  if ( cmsg->cmshg_level == SOL_SOCKET && cmsg->cmshg_type == SCM_RIGHTS ) {
      fd_ptr = (int *) CMSG_DATA(cmshg);
      received_fd = *fd_ptr;
      break;
  }
}

if ( cmsg == NULL ) {
   /* Error: No file descriptor received */
}
```

The general procedure is as follows:

1. The for loop initializes by obtaining the first ancillary data header (struct cmsghdr) using the macro CMSG_FIRSTHDR().
2. The for loop tests whether the pointer cmshg is NULL. The body of the for loop is executed if this pointer is not NULL.
3. The if statement applies two tests to the struct cmsghdr header structure: The program is interested only in messages that are at the cmsg_level equal to SOL_SOCKET and are of the message type SCM_RIGHTS. This identifies an ancillary data object that represents a file descriptor.
4. If the test in step 3 succeeds, the pointer to the file descriptor is stored in pointer variable fd_ptr.
5. The pointer fd_ptr is then used to extract the file descriptor out of the ancillary data buffer into the variable received_fd.
6. The control leaves the for loop with the break statement, because the program has located the information it was interested in.
7. The if statement test that follows the for loop tests the cmsg pointer variable to see whether the ancillary data object was found. If the pointer cmsg is NULL, this indicates the for loop ran until completion without finding the file descriptor. When it is not NULL, this indicates that the break statement was executed, indicating the file descriptor was indeed extracted.

This covers the general outline for extracting data from an ancillary data buffer.

## Creating Ancillary Data

The process that wants to send a file descriptor must create an ancillary data buffer with the correctly formatted data within it. The following code outlines the general procedure:

```c
EXAMPLE
struct msghdr msg;       /* Message header */
struct cmsghdr *cmg;      /* Ptr to ancillary hdr */
int fd;                   /* File descriptor to send */
char buf[CMSG_SPACE(sizeof fd)]; /* Anc. buf */
int *fd_ptr;              /* Ptr to file descriptor */

msg.msg_control = buf;
msg.msg_controllen = sizeof buf;

cmg = CMSG_FIRSTHDR(&msg);
cmg->cmsg_level = SOL_SOCKET;
cmg->cmsg_type = SCM_RIGHTS;
cmg->cmsg_len = CMSG_LEN(sizeof fd);

/* Initialize the payload: */
fd_ptr = (int *)CMSG_DATA(cmg);
*fd_ptr = fd;

/*
 * Sum of the length of all control
 * messages in the buffer:
 */
msg.msg_controllen = cmg->cmsg_len;
```

The general procedure used is as follows:

- The ancillary data buffer was declared to make room to format an ancillary data object (array variable buf[]). Notice that the CMSG_SPACE() macro is used to compute the size of the buffer that is required.
- The message header members msg_control and msg_controllen are initialized to point to the ancillary buffer and assign its maximum length, respectively.
- The pointer cmg is initialized to point at the first ancillary data object within the buffer using the CMSG_FIRSTHDR() macro. Note that the input argument to the macro is the pointer to the message header (&msg) and is not the pointer to the ancillary data buffer.
- The ancillary data object's header is initialized by setting cmg->cmsg_level and cmg->cmsg_type.
- The length of the ancillary data object is established by using the CMSG_LEN() macro with the size of the file descriptor as the input value.
- The pointer to the file descriptor within the ancillary data buffer is determined by using the CMSG_DATA() macro.
- The file descriptor fd is then copied into the ancillary data buffer using the pointer fd_ptr.
- Finally, the total ancillary message length is computed and assigned to msg.msg_controllen.

> **NOTE**
> If there is more than one ancillary data object included, you must be sure that msg.msg_controllen is the sum of all of the parts. Additionally, be certain to sum the total requirements needed for the buffer (buf[] in the example shown).

## Presenting an Ancillary Data Example

Now, it is time to present the software in order to tie all of the concepts together into a concrete example pair of programs. Two programs will be presented:

- A socket server
- A very simple Web server

The Web server will serve one, and only one, simple demonstration HTML page. The socket server will be used to gain access to a port 80 socket without requiring root access or root setup.
