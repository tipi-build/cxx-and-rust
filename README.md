# cxx-and-rust with tipi
This shows how to build C++ and Rust code remotely with [tipi.build](https://tipi.build).

Just install tipi and run : 

## Remote build with caching
* `tipi build . -t linux`

This will ship a remote building environment for Rust that can do Rust build caching.

## Local build 
* `tipi . -t linux`

You should have rustup setup for this though at the moment, and caching is disabled by default.
