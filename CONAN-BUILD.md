# Building libcurl with Conan

## Clean Build
```bash
# Create separate build directory
mkdir -p build && cd build

# Install dependencies (generates CMake files in build dir)
conan install .. --output-folder=. --build=missing

# Configure and build
cmake .. -DCMAKE_TOOLCHAIN_FILE=conan_toolchain.cmake
cmake --build .
```

## Cleanup
```bash
# Remove generated files
rm -rf build/
```



