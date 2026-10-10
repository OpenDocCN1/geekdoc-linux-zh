# # CHAPTER
6

# ## The Hacker’s Technology Handbook

The Hacker’s Technology Handbook contains a collection of the key concepts vital to forming a hacker’s knowledge foundation. Traditionally, learning to hack takes many years of trial and error, technology reference absorption, and study time. This chapter, along with the primers given in Chapters 1 through 3, is designed to be used as a quick reference to that same material, and with review, can reduce that learning curve down to the time it takes to go through this book.

Each section in this chapter corresponds with a step on the path to achieving the basics of a hacker’s education and knowledge. The topics covered include networking concepts, networking technologies, protocols, and important commands. Hacker coding fundamentals are covered in the next chapter.

# ## Networking Concepts

# ### Open Systems Interconnection Model

The International Standards Organization (ISO) developed the Open Systems Interconnection (OSI) Model to describe the functions performed during data communications. It is important to recognize the seven layers that make up the OSI model (see Figure 6.1) as separate entities that work together to achieve successful communications. This approach helps divide networking complexity into manageable layers, which in turn allows specialization that permits multiple vendors to develop new products to target a specific area. This approach also helps standardize these concepts so that you can understand all of this theory from one book, as opposed to hundreds of publications.

+   - **Layer 7: Application.** Providing the user interface, this layer brings networking to the application, performs application synchronization and system processes. Common services that are defined at this layer include FTP, SMTP, and WWW.

+   - **Layer 6: Presentation.** Appropriately named, this layer is responsible for presenting data to layer 7. Data encoding, decoding, compression, and encryption are accomplished at this layer, using coding schemes such as GIF, JPEG, ASCII, and MPEG.

+   - **Layer 5: Session.** Session establishment, used at layer 6, is formed, managed, and terminated by this layer. Basically, this layer defines the data coordination between nodes at the Presentation layer. Novell service access points, discussed in Chapter 2 and NetBEUI are protocols that function at the Session layer.

+   - **Layer 4: Transport.** TCP and UDP are network protocols that function at this layer. For that reason, this layer is responsible for reliable, connection-oriented communication between nodes, and for providing transparent data transfer from the higher levels, with error recovery.

+   - **Layer 3: Network.** Routing protocols and logical network addressing operate at this level of the OSI model. Examples of logical addressing include IP and IPX addresses. An example of a routing protocol defined at this layer is the Routing Information Protocol (RIP; discussed later).

+   - **Layer 2: Data Link.** This layer provides the reliable transmission of data into bits across the physical network through the Physical layer. This layer has the following two sublayers: