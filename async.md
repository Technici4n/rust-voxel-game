# Asynchronous event handling
If you have a look at modded Minecraft servers, they often end up lagging behind as more and more chunks are kept artificially loaded.
The principal reason for this is that many blocks keep checking for updates every _tick_ (0.05s).
The solution to this problem would be to invoke callbacks on specific event fires or after some delay instead of checking for updates 20 times a second.

**Example**: have a look at a furnace. Clearly, it doesn't need to be updated every tick (unless its GUI is opened, and even then it's on the client side). What one could do instead is tracking the following events:
* The burning item is removed (event).
* The furnace is destroyed (event).
* The furnace runs out of fuel (timer).
* The burning item is done _cooking_ (timer).
* And so on...

Of course, it is harder to implement but with proper scheduling and careful thinking it is all but impossible.