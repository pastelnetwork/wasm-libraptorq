# Linux wasm libraptorq build

To Build RaptorQ library comment in CMakeLists.txt lines: 
```
COMMAND make_deterministic
```
With emcc compiler is not possible to run this commands besouse it will be wasm module.

Then use cmake to create Makefile with configuration for emcc:

```
cmake -DCMAKE_BUILD_TYPE=Release \
 -DRQ_ENDIANNESS=LittleEndian \
 -DTEST_BIG_ENDIAN=0 \
 -DPROFILING=OFF \
 -DDYNAMIC_LIB=OFF \
 -DCMAKE_C_COMPILER={path_to_emscripten}/emcc \
 -DCMAKE_CXX_COMPILER={path_to_emscripten}/em++ \
 ../
```

Compile wasm module with bindings and raptorq:
```
sh build.sh
```
