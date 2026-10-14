
how the base station mote sets itself up as the root of the collection tree to report theft settings to the PC, and how it disseminates new settings received from the PC. Chapter 7 presents the PC-side of the mote connection.

## 6.4.1 Collection

Sending a message via a collection tree is very similar to using AM, except that messages do not have a destination address (the tree root is the implicit destination). Thus collection trees use the Send interface, which is identical to AMSend except for the lack of an addr parameter to the send command:

```
interface Send {
  command error_t send(message_t* msg, uint8_t len);
  event void sendDone(message_t* msg, error_t error);
  command error_t cancel(message_t* msg);

  command uint8_t maxPayloadLength();
  command void* getPayload(message_t* msg, uint8_t len);
}
```

Listing 6.18  The Send interface

As a result, the code in MovingC for reporting a theft over a collection tree is nearly identical to that from Section 6.3.1:

```
uses interface Send as Theft;
...
message_t reportMsg; // The theft report message buffer
bool sending;        // Don't try and send while a send is in progress

void reportTheft() {
  theft_t *payload = call Theft.getPayload(&reportMsg, sizeof(theft_t));

  if (payload && !sending)
    { // We can send if we're idle and the payload fits
      payload->who = TOS_NODE_ID; // Report that *we* are being stolen!
      // And send the report to the root
      if (call Theft.send(&reportMsg, sizeof(theft_t)) == SUCCESS)
        sending = TRUE;
    }
}

event void Theft.sendDone(message_t *msg, error_t error) {
  sending = FALSE; // Our send completed
}
```

Listing 6.19  Anti-Theft: reporting theft over a collection tree

## 6.4.2 Dissemination

The dissemination service is accessed by an interface parameterized by the type of value being disseminated:

```
interface DisseminationValue<t> {
  command const t* get();
  command void set( const t* );
  event void changed();
}
```

Listing 6.20 DisseminationValue interface

The dissemination values are sent across the network, so the type passed to DisseminationValue should be a platform-independent type (Section 3.5.3). In our case, we reuse the settings_t type we defined in Section 6.3.2, which contains new acceleration variance and check intervals. The code in MovingC to receive and handle new settings is simple:

```
uses interface DisseminationValue<settings_t> as Settings;
... 
/* New settings received, update our local copy */
event void Settings.changed() {
  const settings_t *newSettings = call Settings.get();
  accelVariance = newSettings->accelVariance;
  call TheftTimer.startPeriodic(newSettings->accelInterval);
}
```

Listing 6.21 Anti-Theft: settings via a dissemination tree

## 6.4.3 Wiring collection and dissemination

Like AM itself, the collection and dissemination services must be explicitly started, this time via the non-split-phase StdControl interface:

```
interface StdControl {
  command error_t start();
  command error_t stop();
}
```

Listing 6.22 The StdControl interface

Furthermore, as they are built over AM, the radio must be started first. As a result, the AntiTheft boot sequence is now slightly more complex (as earlier, we don’t check error codes as there is no obvious recovery step):

```
uses interface SplitControl as CommControl;
uses interface StdControl as CollectionControl;
uses interface StdControl as DisseminationControl;
...
event void Boot.booted() {
  call CommControl.start();
}
```

```
event void CommControl.startDone(error_t ok) {
  // Start multi-hop routing and dissemination
  call CollectionControl.start();
  call DisseminationControl.start();
  // Start checks once communication stack is ready
  call TheftTimer.startPeriodic(ACCEL_INTERVAL);
}
```

AM types identify different kinds of messages in a mote network. In a similar fashion, collection and dissemination use 8-bit identifiers to allow for multiple independent collection trees and for multiple values to be disseminated. As with AM, these identifiers are specified as arguments to the CollectionSenderC and DisseminatorC generic components that provide access to collection and dissemination:

```
enum { COL_THEFT = 54, DIS_THEFT = 55 };
...
```

```
components ActiveMessageC, DisseminatorC, CollectionC;
MovingC.CommControl -> ActiveMessageC;
MovingC.CollectionControl -> CollectionC;
MovingC.DisseminationControl -> DisseminationC;
```

```
/* Instantiate and wire our collection service for theft alerts */
components new CollectionSenderC(COL_THEFT) as TheftSender;
MovingC.Theft -> TheftSender;
```

```
/* Instantiate and wire our dissemination service for theft settings */
components new DisseminatorC(settings_t, DIS_THEFT);
MovingC.Settings -> DisseminatorC;
```

## 6.4.4 Base station for collection and dissemination

For collection and dissemination to be useful, something must consume the messages sent up the collection tree, and produce new values to disseminate. In the case of AntiTheft, we assume a PC with a serial connection to a base station mote displays theft reports and allows the theft detection settings to be changed. Here we just show how the base station mote is setup to forward tree collection theft reports and disseminate theft settings; Chapter 7 presents the libraries and utilities that are used to write PC applications that communicate with mote networks.
