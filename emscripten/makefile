EMSCRIPTEN_VERSION=1.37.22
EMSCRIPTEN_BITS=64bit
EMDOCKER_IMAGE=trzeci/emscripten:sdk-tag-$(EMSCRIPTEN_VERSION)-$(EMSCRIPTEN_BITS)

.PHONY: all

OPTIMIZE+=-O2

CFLAGS +=  -Wall -Werror -Iinclude -fno-strict-aliasing $(OPTIMIZE)
CXXFLAGS += -Wall -Werror --std=c++11 $(OPTIMIZE)

CFLAGS += -msse2

EXPORTED_FUNCTIONS=-s EXPORTED_FUNCTIONS='["_blake", "_hmac_blake224_hash", "_hmac_blake256_hash", "_blake256_hash", "_blake_hash", "_blake224_hash"]'
EMSCRIPTEN_SETTINGS=-s "BINARYEN_METHOD='native-wasm'" -s WASM=1 -s  DISABLE_EXCEPTION_CATCHING=1 \
				     -s NO_FILESYSTEM=1 $(EXPORTED_FUNCTIONS) \
				      --post-js emscripten/emscripten.blake.post.js
EM_CC_COMPILER  = docker run -v $(CURDIR)/../:/src $(EMDOCKER_IMAGE) emcc $(EMSCRIPTEN_SETTINGS)
EM_CXX_COMPILER = docker run -v $(CURDIR)/../:/src $(EMDOCKER_IMAGE) em++ $(EMSCRIPTEN_SETTINGS)


all: clean ../dist/emscripten/blake.js



../dist/emscripten/blake.js: 
	@mkdir -p ../dist/emscripten
	$(EM_CC_COMPILER) $(CFLAGS) -o dist/emscripten/blake.js src/blake.c 

clean:
	rm -f build/emscripten/*
