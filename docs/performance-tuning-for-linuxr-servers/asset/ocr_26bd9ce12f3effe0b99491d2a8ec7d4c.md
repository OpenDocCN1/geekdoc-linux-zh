```
3XMTHREADINFO  "Service Engi neTransports : 369" (TID: 0x103390)  .Sys_ _Thread_,1,0x414DB05, _state_:R, _native\_
ID:0x64CU8)  prios=5
4XESTACKTRACE  at COM.ibm.db2.jcc.apg.DB2XAResource.<active min_>(Naive Method)
4XESTACKTRACE  at COM.ibm.db2.jcc.apg.DB2XAResource.commin DB2XAResource_ j.<init(Compiled Code))
4XESTACKTRACE  at com.ibm.wss.rad.apg.tp.WSRCAckracer_dialy(commin WSRCSAckracer_dialy.java:204_(Compil
e))
4XESTACKTRACE  at com.ibm.wss.rad.apg.trx.6XTransactionWrapper,comminXAResource_)(Compliled Code)
4XESTACKTRACE  at
com.ibm.wss.TransactionJTAJATXAResourcepl.commin_gl_phase_plJATXAResource commin pl.java:(Compiled
Code)
4XESTACKTRACE  at com.ibm.wss.TransactionJTARegisteredResources.lFlow.Commn(RegisteredResource. java:(Compiled Code))
4XESTACKTRACE
com.ibm.wss.TransactionJTARegisteredResources.distribut ePrepare(RegisieredReSOurces. java:(Compiled Code))
4XESTACKTRACE  at com.ibm.wss.TransactionJTA.TranSACTIONimpl.contin ue(PrepareTransactionimpl.java:(Compliled Code))
4XESTACKTRACE  at com.ibm.wss.TransactionJTA.TransactionImpl.commitTransactionimpl.java:(Compiled Code))
4XESTACKTRACE  at com.ibm.wss.TransactionJTA.TransManagerlf.comminITransManagerImpl java:(Compiled Code)
4XESTACKTRACE  at com.ibm.wss.TransactionJTA.TransManagerlf.comminT1ransManager,java:(Compiled Code)
4XESTACKTRACE  at com.ibm.db2. iJcc.DB2Strategg.commiti2TransStrategy-java:(Compiled Code)
4XESTACKTRACE  at com.ibm.db2. iJ.cc.DB2Strategy. postinvoke(TransStrategy.java:(Compiled Code))
4XESTACKTRACE  at com.ibm.db2.iJ.cc.Translaction_controlImpl. postinvoke(Transaction controlimpl.java: Compiled Code)
4XESTACKTRACE  at com.ibm.db2.ic.contrailer.EEIGc_statater_postinvoke(EESc_state.java:(Completed Code))
4XESTACKTRACE  at com.ibm.db2.iJ.cc.contracler EESc_statater_postinvoke(EESc_statetor java:(Compiled Code))
4XESTACKTRACE  at com.ibm.ws.oibpetor.sample.trade.jib.JiPilot commin TradeJIB.952-104:Jcc:1 getComnitedKnowno
_ Source()
4XESTACKTRACE  at com.ibm.webshpere, sample, trade, 0_2B_ Trade_Sink_ getlnoic_Trade.java:(Completed Code)
4XESTACKTRACE  at com.ibm.webshpere, sample, trade, commin command, QueryCommindeitforminBasisic_5k)(Compiled
Code)
4XESTACKTRACE  at com.ibm.webshpere.command.Localtarge, execateCommandL.o.0i target.java:(Compiled Code))
4XESTACKTRACE  at com.ibm.ws, cc,he.commnniCommandExecuteCommandComminni Command, execjava_(Compliled
4XESTACKTRACE  Code))
com.ibm.ws.webshpereator, ccapp.WebAppRequestDispatcher.handle(WebAppRequest:java:WebAppRequest. java:(Compiled
Code))
```

We examined all of the threads, and none of them are in the MW state. In fact, all threads that are in the JDBC code are in the R state. We can conclude that the database server is not a bottleneck because none of the threads is blocked by it.

# Database I/O Activity

The next step is to check the I/O activity at the database server. We ran the same test and used **iostat** on the database server:

```
iostat -d 2
```

This command monitors the disk activity every 2 seconds. Following is a segment of the trace:

```
Device: tps Blk_read/s Blk_wrt n/s Blk_read Blk_wrt n
dev3-0 39.00 0.00 400.00 0 800

Device: tps Blk_read/s Blk_wrt n/s Blk_read Blk_wrt n
dev3-0 32.50 0.00 480.00 0 960

Device: tps Blk_read/s Blk_wrt n/s Blk_read Blk_wrt n
dev3-0 49.00 0.00 504.00 0 1008

Device: tps Blk_read/s Blk_wrt n/s Blk_read Blk_wrt n
dev3-0 33.00 0.00 356.00 0 712

Device: tps Blk_read/s Blk_wrt n/s Blk_read Blk_wrt n
dev3-0 33.50 0.00 380.00 0 760
```