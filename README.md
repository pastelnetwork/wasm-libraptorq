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
 -DPROFILING=OFF \
 -DDYNAMIC_LIB=OFF \
 -DCMAKE_C_COMPILER={path_to_emscripten}/emcc \
 -DCMAKE_CXX_COMPILER={path_to_emscripten}/em++ \
 ../
```

Compile wasm module with bindings and raptorq:
```
em++ bind.cpp libRaptorQ.a librq_lz4_static.a \
    -IRaptorQ \
    --bind \
    -s ALLOW_MEMORY_GROWTH=1 \
    -s MEMORY_GROWTH_GEOMETRIC_STEP=1 \
    -s WASM=1 -s EXIT_RUNTIME=0 -s INVOKE_RUN=0 \
    -s MODULARIZE=1 \
    -s FETCH=1 \
    -s EXPORT_NAME=RaptorQ \
    -flto -O3 \
    -o raptorq.js
```
