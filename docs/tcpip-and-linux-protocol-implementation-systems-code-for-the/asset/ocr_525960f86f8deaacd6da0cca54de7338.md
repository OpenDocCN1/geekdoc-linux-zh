# 276 TCP/IP and Linux Protocol Implementation

320

321

```
copied = skb->len;
if (copied > len) {
    msg->msg_flags |= MSG_TRUNC;
    copied = len;
}
err = memcpy_toovec(msg->msg_iov, skb->data, copied);
if (err) {
    goto out_free_skb;
}
sock_recv_timestamp(msg, skb);
serr = SK_EXT_ERR(skb);
sin = (struct sockaddr_in *)msg->msg_name;
if (sin) {
    sin->sin_family = AF_INET;
    sin->sin_addr.s_addr = *(u32*)(skb->nh.raw + serr->addr_offset);
    sin->sin_port = -serr->port;
}
```

322

323

324

325

326

327

328

329

330

331

332

333

334

335

336

337

338

339

![](bbox=[0.115, 0.435, 0.915, 0.465])

341

342

```
memcpy(&errhdr, ee, min(ee, sizeof(struct sock_extended_err)));
sin = errhdr.offset;
sin->sin_family = AF_UNSPEC;
if (serr->ee.se_origin == SO_EE_ORIGIN_ICMP) {
    sin->sin_family = AF_INET;
    sin->sin_addr.s_addr = skb->nh->saddr;
}
if (sk->protoinfo->of.inet.ip_flags) {
    ip_rcvw(msg, skb);
}
```

343

344

345

346

347

348

349

350

351

352

```
/* Now we could try to dumped packets options */
```

353

354

```
msg->msg_flags |= MSG_ERRQUEUE;
```

```
err = copied;
```

355

356

357

```
/* Reset and regenerate socket error */
```

358

359

```
spin_unlock_irq(&sk->error_queue.lock);
```

360

361

362

```
if ((skb2 = skb_peek(sk->error_queue)) != NULL) {
    sk_error = SK_EXT_ERR(skb2)->se.errno;
    spin_unlock_irq(&sk->error_queue.lock);
}
```