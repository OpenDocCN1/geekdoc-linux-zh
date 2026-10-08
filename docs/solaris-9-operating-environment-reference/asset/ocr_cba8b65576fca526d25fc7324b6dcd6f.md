# ll2_stats

uiSent The number of Unnumbered Information Frames sent.

uiRcvd The number of Unnumbered Information Frames received.

outOfState The number of events received in an invalid state.

state.allocFail The number of buffer allocation failures.

protocolError The number of LLC protocol errors, that is, the receipt of malformed PDUs or the receipt of frame X when frame Y was expected.

In the following example, 10 established connections are associated with this SAP. The following command retrieves the statistics for connection 1.

```
example@ /usr/lib/llc2/llc2_stats 4 -s 2 -c 1
Connection values received:
ppa = 0x0004
clearFlag = 0x00
sap = 0x02
con = 0x0001
sid = 0x0201
stateOldest = 0x00
stateOld = 0x00 stateOld = 0x01
state = 0x08
dl_nodeaddr = 0x0080d84008c2
dl_sap = 0x04
flag = 0x50
dataFlag = 0x00
timerOn = 0x18
vs = 0x29
vr = 0x1e
nrRcvd = 0x029 k = 0x14
retryCount = 0x0000
numToBecked = 0x0000 numToResend = 0x0000
macOutSave = 0x0000
macOutDump = 0x0000
iSent = 0x0ba9
iRcvd = 0x001e
fmrSent = 0x0000
fmrRcvd = 0x0000
nrSent = 0x016a
nrRcvd = 0x00c1
nnrSent = 0x0000
nnrRcvd = 0x06fb
rejSent = 0x0000
rejRcvd = 0x0000
sabmeSent = 0x0000
sabmeRcvd = 0x0001
uuaaSent = 0x0001
uaRcvd = 0x0000
discsSent = 0x0000
outOfState = 0x0000
```