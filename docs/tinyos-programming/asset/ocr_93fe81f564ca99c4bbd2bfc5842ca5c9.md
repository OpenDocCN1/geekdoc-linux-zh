individual operation is unpredictable: some arbitrary set of operations from other users may happen between your request and its actual execution. Some virtualized drivers may however offer some specific guarantees, e.g. the AMSenderC instances handle their users in a round-robin fashion.

Shared drivers offer a workaround to the unpredictable latency of virtualized drivers. Shared drivers use the Resource interface (Section 11.2) to control access by multiple users, and once a user has been granted access to the driver, that user's operations are executed immediately. Each user is identified by a unique id, obtained using nesC's unique() function (Section 9.1). This id is then used to parameterize both the Resource and functional interfaces, to easily distinguish each user's commands and events, as in the Stm25pSectorC, the HAL driver for the ST M25P flash chip:

```
configuration Stm25pSectorC {
  provides interface Resource as ClientResource[uint8_t id];
  provides interface Stm25pSector as Sector[uint8_t id];
  provides interface Stm25pVolume as Volume[uint8_t id];
}
```

Users of Stm25pSectorC must request access via the ClientResource interface before making any requests to read, write, or erase the flash via Stm25pSector:

```
char mybuf[16];

void readMybuf() {
  /* Request access before starting the read */
  call FlashResource.request();
}
```

```
event void FlashResource.granted() {
  /* We have access, we can now do our read */
  call Stm25pSector.read(0, mybuf, sizeof mybuf);
}
```

```
event void Stm25pSector.readDone(...) {
  /* Release the resource now that we're done */
  call FlashResource.release();
  ... use mybuf ...
}
```

More complex code might perform multiple operations using Stm25pSector before releasing access to the flash. Note, however, that performing many long operations will increase the latency before which other flash users can perform any operations at all. As compared to virtualized drivers, shared drivers have predictable latency for operations performed when access has been granted. The cost is extra code complexity to manage the explicit driver request and release operations, and a possibly longer latency until the first operation can be executed.

Wiring to a shared driver such as Stm25pSectorC is generally straightforward. A client id is picked using unique(), and the functional and Resource interfaces are then