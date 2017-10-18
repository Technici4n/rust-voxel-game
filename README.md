# Rust Voxel Game Project
This is the description of a project to create a full, moddable, yet free and open source, voxel game in Rust.

Little has been done, and I don't expect anyone to contribute to this project for now. I would just like to hear input on my ideas in order to find better solutions that I couldn't have thought of myself.

Feel free to suggest any improvement, of the ideas or of sections the document itself (like spelling mistakes).

## The idea

### Goals
* Creating a voxel engine/game like Minecraft, Minetest, ...
* Making it fully moddable.
* Making it totally safe.
* Making it **very** fast, even with a consequent amount of loaded mods.
* Exploring Rust as a game programming language, as it focuses on safety while maintaining execution speed.
* Exploring plugin loading in Rust.
* Only relying on "pure Rust" solutions, whenever it makes sense (for Operating Systems it doesn't ;-)).
* Broadening the Rust ecosystem.

### Non-goals
* Providing a very high level modding interface. The project should follow Rust's zero cost abstraction principle when possible.
* Probably others...

### Design elements
* Modern OpenGL using buffers to improve rendering performance
* [Multi-threaded client and server](client_server.md)
* [Asynchronous event handling](async.md)
* [Mod loading (input asked)](mods.md)

## Short-term priorities
* Implementing chunk rendering and basic generation (flat world).
* Publish the source code on Github.
* Implementing a basic GUI.
* Implementing basic networking.
* Block placing and breaking.
