```
			case -1:
				EC_FAIL
			}
		ec_false( ev_creat() )
		ec_false( pt_wait_master(p) )
```

I put the stuff having to do with redirecting file descriptors and executing a com-
mand in the function `exec_redirected` because I’m going to explain it all in
Chapters 5 and 6. I will show the code for `exec_redirected`, however, without
explaining it. You can come back to it after reading those chapters if you need to.

The code so far in `main` takes us to step 9 (explained in the previous section),
which is when we begin reading and writing the pt’s master-side file descriptor.
Bear in mind that the subject command (`script1`, `vi`, or whatever) is already
running and is probably blocked in a `read` waiting for some input from what it
thinks is a terminal. Here’s the rest of the `main` function:

```
		tc_setraw();
		while (true) {
			fd_set fd_set_read;
			char buf[EVBUFSIZE];
			ssize_t nread;

			FD_ZERO(&fd_set_read);
			FD_SET(STDIN_FILENO, &fd_set_read);
			FD_SET(PT_GET_MASTER_FD(p), &fd_set_read);
			ec_negl( select(PD_SETSIZE, &fd_set_read, NULL, NULL, NULL) )
			if (FD_ISSET(STDIN_FILENO, &fd_set_read) ) {
				ec_negl( nread = read(STDIN_FILENO, &buf, sizeof(buf)) )
				ec_negl( writeall(PT_GET_MASTER_FD(p), buf, nread) )
			}
			if (FD_ISSET(PT_GET_MASTER_FD(p), &fd_set_read) ) {
				if ((nread = read(PT_GET_MASTER_FD(p), &buf,
				sizeof(buf))) > 0) {
					ec_false( ev_write(buf, nread) )
					ec_negl( writeall(STDOUT_FILENO, buf, nread) )
				} else if (nread == 0 || (nread == -1 && errno == EIO))
					break;
				else
					EC_FAIL
			}
		}
		ec_negl( ev_write(NULL, 0) )
		fprintf(stderr,
			"EOF or error reading stdin or master pseudo-terminal; exiting\n");
		ok = true;
```