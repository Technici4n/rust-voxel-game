# Client and Server architecture
The client and server should be multithreaded, yet completely data race safe thanks to Rust's guarantees: the threads would communicate using channels to pass messages and data strctures around.

## Client
The client consists of 3 threads. Both the main and the rendering thread would hold a copy of the loaded chunks, to make synchronisation easier.

### Main thread
Where rendering happens.
This thread is also responsible for handling user input, for playing sound, ...

It mostly sends messages to the network thread, and tells the meshing thread to drop chunk information when they get unloaded.

### Network thread
Where (asynchronous) network I/O happens.

This thread downloads chunks and block updates from the server, sends the player's position to the server, ...
Therefore, it must send messages to the 2 other threads.

### Meshing thread
Where meshing happens.

Whenever this thread receives block updates, it generates the new buffers (only the visible faces) from the chunks and sends the updated Vecs to the client.

## Server
The server consists of 3 threads. It would be possible to add a world generation thread.

### Main thread
Core of the engine.
This thread contains the game loop, which constantly updates loaded chunks.

### Network thread
Network I/O.

### Disk I/O thread
This thread is responsible for loading and saving chunks as necessary. Since this operation can be long, it is reasonable to keep it in a separate thread. The I/O could eventually be made asynchronous.