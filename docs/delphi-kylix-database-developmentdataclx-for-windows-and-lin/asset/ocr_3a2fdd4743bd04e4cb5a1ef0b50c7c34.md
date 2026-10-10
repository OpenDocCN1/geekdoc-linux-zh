A better way to code for this situation is to handle the `BeforeDelete` event and display a message there asking the user if he is sure he wants to delete the record. As with most `BeforeXxx` event handlers, raising an exception (usually `Abort`) inside the event handler prevents the operation from taking place.

Later in this section, I’ll present a sample application that illustrates this technique. Table 4.1 lists the client dataset’s `BeforeXxx` events and their uses.

| Event | Description |
| --- | --- |
| **BeforeCancel** | Triggered by the `Cancel` method just before the edits to the current record are canceled. You might take advantage of this event to confirm that the user does indeed want to cancel any changes that he has made. |
| **BeforeClose** | Called immediately before the dataset is closed. |
| **BeforeDelete** | Called just before the current record in the dataset is deleted. This is a good place to confirm that the user really wants to delete the record. |
| **BeforeEdit** | Triggered by the `Edit` method immediately before the dataset is put into edit mode. You could use this event as a handy place to restrict editing (by raising an `Abort` exception). |
| **BeforeInsert** | Triggered by the `Append` and `Insert` methods immediately before the dataset is put into insert mode. You could use this event as a way to restrict editing (by raising an `Abort` exception). |
| **BeforeOpen** | Called just before the dataset is opened. |
| **BeforePost** | Occurs just before the data in a newly inserted or edited record is posted to the dataset. This is a good place to perform validation on the data. |
| **BeforeScroll** | Triggered just before the dataset moves to a new record. This occurs when the dataset is opened during a `First`, `Next`, `Prior`, or `Last` operation; during searches; and when a range or filter is applied to the dataset. |

In contrast to the `BeforeXxx` event handlers, which are triggered before an event actually occurs (and therefore enable you to prevent the event from occurring), `AfterXxx` event handlers are triggered after the event has occurred to let you know that the operation in question has occurred successfully. Table 4.2 lists the `AfterXxx` event handlers, which mirror the `BeforeXxx` event handlers.

# 4 ADVANCED CLIENT DATASET OPERATIONS