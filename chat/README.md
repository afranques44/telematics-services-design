# Chat

Multi threaded instant messaging application in Java. Capable of sending and receiving messages between two machines across the network, as well as performing file transfers.

When the application starts, it asks for the IP address of the other end, and although it could also ask for the port number used, this has already been predefined in the code. The transport protocol chosen for the exchange of packets is TCP. The packets corresponding to a possible file transfer are sent through the same socket (instead of using a new one) than the ones corresponding to the regular chat messages, therefore the code has to deal with distinguishing both packet types. The file transfer occurs in a background thread, created at the moment of the file transfer startup (when **@rchivo** is invoked), allowing this way that both ends keep chatting in foreground.

###Chat commands:

- **@rchivo** - when either of the two ends invokes this command, it calls the file transfer procedure, i.e. it asks to the caller what is the name of the file to be transferred, it asks the other user by what name does it want to save the receiving file, it starts transferring the file into a background thread, it notifies both ends that the transfer has started (and they can continue chatting meanwhile), and it notifies both ends when the transfer finishes.
- **fin** - when either of the two ends invokes this command, the connection is terminated (although if there's a file transfer going on, it first asks the user for confirmation), and it's also notified to the other end that it's messages will no longer be received by the other end.

_A fairly detailed description of the code structure can be found at memoria.pdf, although it's in Spanish. I will soon start translating it to English. However, I originally wrote the code (comments and variable names) in Spanish, and that will probably still make it hard to read for most part of the people._

### Screenshots:

The screenshots show a conversation between two users; a _client_ and a _server_. Also, the _client_ sends the file _lorem_ipsum.txt_ to the _server_, who saves the file as _lorem_ipsum_rx.txt_. Finally, the _server_ terminates the conversation and the last message from _client_ is never received by _server_.

- **Client**

![Client](/chat/screenshots/chat_conversation_screenshot_client.png "Client")

- **Server**

![Server](/chat/screenshots/chat_conversation_screenshot_server.png "Server") 

