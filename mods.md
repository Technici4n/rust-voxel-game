# Mod loading
Just like Minetest, the engine itself should not provide any game content, but rather convenience and compatibility interfaces.

Different mod loading strategies are possible. I've listed the pros and cons of every one. I only wrote what came to my mind. As suck, there may be others and I might be wrong. I'll be happy to talk about it.

The server could send the client information about native mods, or the mods' scripts directly.

## Scripting language integration
It is possible to rely on some interpreted language for modding, like Lua.

### Pros
* No binaries
* Hot code reloading
* Higher level
### Cons
* FFI interactions are complicated and unsafe, it might be annoying and error-prone to write wrapper C functions around Rust constructs. Let only load shared library code.
* Performance

## Native language integration (dynamic loading)
It is also possible to directly load Rust mods at runtime.

### Pros
* Performance
* Faster compilation than static loading

### Cons
* Safety (on the hosting system): it's harder/impossible to restrict file system access.
* Unsafe interactions
* The borrow checker may not like it.

## Native language integration (static loading)
A binary could be built using a specific of mods in the form of Rust modules. A script could generate a file that links them together with the engine.

### Pros
* Performance
* Easier library interfacing
* No FFI
### Cons
* Safety on the host system.
* Harder installation (requires rust on the user's system) or fewer configuration.
* Linking time in development cycles (could be solved with `prefer-dynamic`)