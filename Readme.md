#  HMAC-BLAKE-256 and HMAC-BLAKE-224 implementation and compile-2-wasm library

The blake256_* and blake224_* functions are largely copied from
blake256_light.c and blake224_light.c from the BLAKE website:

     http://131002.net/blake/

The hmac_* functions implement HMAC-BLAKE-256 and HMAC-BLAKE-224.
HMAC is specified by RFC 2104.


# Purpose #
static library which would be used for further iterative modifications/optimizations and cross-compiled to few other non-standard platforms, like 'browser's asm.js (see emscripten folder in project root)

# howto
`cmake .` and `make ` should work for you. CLion should autogenerate build targets if you import project from source. 

For wasm compilation you need either:
- docker installed on pc (see emscripten/makefile) to build wasm and wrappers using emscripten SDK
- npm, build-tools-essential, clang, cmake to build wasm using node-webassembly project (see package.json for details)


