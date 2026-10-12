![](bbox=[0.25, 0.1, 0.75, 0.23])

**Figure 18.4** Building Services—bookings on date

is received it should ignore the date, and instead iterate over all the bookings, accumulating a list of the dates for which the given room is booked. If there are no bookings, it should return an error reply. Otherwise, instead of using the sendReply() method, it should send its own byte array with its length, the action, the room string, and then a 32-bit integer containing the number of dates in the list, followed by each of the dates. Since the dates are stored as datetime.date objects, they must be converted to QDates to stream them into the QByteArray.

![](bbox=[0.25, 0.43, 0.75, 0.57])

**Figure 18.5** Building Services—bookings for room

The Building Services client must be modified to provide a Bookings for Room? button, connected to a method that issues a suitable request. The client's readResponse() method will need to be modified so that if a BOOKINGSFORROOM response is received, it reads in the dates and creates a suitable string for display in the client user interface, as shown in Figure 18.5.

The modifications to the server can be done by adding about 30 lines, and to the client by adding about 40 lines. However, the BOOKINGSFORROOM request/response does require some care.

Solutions are provided in chap18/buildingservicesserver_ans.pyw and chap18/buildingservicesclient_ans.pyw.