```
CONNECT bhvr_class bhvr_name TO bhvr_class bhvr_name port | HOOK
hook_name END
```

connects the input of the bhvr_name instance to the output, port. of the specified instance following next, or to the specified hook, hook_name. One single instance can be connected to several outputs or hooks. However, only one single component instance can be appended to each output or hook.

```
DISCONNECT bhvr_class bhvr_name port END
```

deletes the connection on the specified output. The REMOVE command can delete a component instance only provided that all links have been deleted.