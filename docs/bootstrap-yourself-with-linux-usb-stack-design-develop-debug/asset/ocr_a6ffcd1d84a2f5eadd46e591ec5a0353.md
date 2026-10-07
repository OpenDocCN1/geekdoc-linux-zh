# Chapter 13 = Gadget Driver

```
unsigned long flags;
int request = 0;
ep = container_of(_ep, struct r8a66597_ep, ep);
req = container_of(_req, struct r8a66597_request, req);
if (ep)->r8a66597->gadget.speed == USB_SPEED_UNKNOWN) {
    return -ESHUTDOWN;
nsspin_lock_irqsave(&ep->r8a66597->lock, flags);
if (list_empty(&ep)->queue)) {
    request = 1;
    list_add_tail(&req->queue, &ep->queue);
}
req->req.actual = 0;
req->req.status = -EINPROGRESS;
if (ep)->desc == NULL) { /* control */
    start_0p(ep, req);
}
else {
    if (request && !ep->busy) {
        start_packet(ep, req);
    }
spin_unlock_irqrestore(&ep->r8a66597->lock, flags);
}
return 0;
}
static int r8a66597_dequeue(struct usb_ep *_ep, struct usb_request *_req) {
    struct r8a66597_ep *ep;
struct r8a66597_request *req;
ununsigned long flags;
ep = container_of(_ep, struct r8a66597_ep, ep);
req = container_of(_req, struct r8a66597_request, req);
spin_lock_irqsave(&ep->r8a66597->lock, flags);
if (!list_empty(&ep)->queue)) {
    transfer_complete(ep, req, -ECONNRESET);
    spin_unlock_irqrestore(&ep->r8a66597->lock, flags);
    return 0;
}
```

These two functions act as the essential backbone of the gadget framework for OUT and IN transfer. You can explore other callbacks from r8a66597-udc.c along with the datasheet r8a66597 to better understand the sequence of activities carried out in the driver framework.