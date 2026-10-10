One thing is important to note: no layer that receives data alters the information but adds information that aids in its reaching its destination. In the Presentation layer, information about the formatting of data takes place so as to ensure that the same layer at the destination computer is able to read. For the most part, it identifies the type of data apart from the application that will be able to read it.

A simple example of this involves the sending of a PDF document from a Windows 10 to an Ubuntu system. Not only will the Presentation layer determine the MIME type (pdf in this case) but will add this information in the header as it sends the data to the Session Layer.

When it reaches the receiver's computer, the Presentation Layer is able to identify the file type by reading the header and which results in a PDF viewer being opened to view the file. This layer also helps with encryption and compression of files where the information pertaining to these two aspects is added for the Presentation layer on the destination system so the file can be decrypted and decompressed. That said, if your computer does not have an application that can open the file, the Presentation Layer in your system will only display an unassociated icon.

# Layer 5: Session

Once the protocol data unit is passed on to this layer, it works to initiate a connection with an application or service on the receiver's system apart from maintaining and closing the connection after the data has been transmitted. As for the information it adds about the application or service that it has to make a connection with, this includes a port number and after which, the protocol data unit is passed on to the transport layer.

As for the connections that this layer seeks to make, they consist of three types:

+   Simplex - Communication that takes place in one direction