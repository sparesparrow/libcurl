# libcurl - HTTP Library Integration

## 📦 Package Overview
- **Name**: `libcurl` (consumer package)
- **Purpose**: HTTP library for integration testing with OpenSSL
- **Build System**: CMake with Conan integration

## 🔄 Conan Build Workflow

### Clean Build Process
```bash
# 1. Create separate build directory
mkdir -p build && cd build

# 2. Install dependencies (generates CMake files in build dir)
conan install .. --output-folder=. --build=missing

# 3. Configure and build
cmake .. -DCMAKE_TOOLCHAIN_FILE=conan_toolchain.cmake
cmake --build .
```

### Cleanup Process
```bash
# Remove generated files
rm -rf build/
```

## 📋 Generated Files (Gitignored)

### Conan Generated Files
- `*.cmake` - CMake integration files
- `conan*.sh` - Environment setup scripts
- `deactivate_*.sh` - Environment cleanup scripts
- `conan*.txt` - Conan configuration files
- `conanbuild/` - Build environment directory
- `conanrun/` - Runtime environment directory
- `CMakeUserPresets.json` - CMake presets

### Why These Are Gitignored
- **Build Artifacts**: Generated during build process
- **Environment Specific**: Different per build environment
- **Temporary**: Recreated on each build
- **Source Pollution**: Should not be in source control

## 🏗️ Build Configuration

### conanfile.txt
```ini
[requires]
openssl/3.6.0

[generators]
CMakeDeps
CMakeToolchain
```

### CMake Integration
- Uses `conan_toolchain.cmake` for toolchain configuration
- Uses `CMakeDeps` for dependency management
- Links against OpenSSL libraries

## 🧪 Testing Integration

### Purpose
- **Integration Testing**: Verify OpenSSL works with HTTP clients
- **Real-world Usage**: Test OpenSSL in practical scenarios
- **Dependency Validation**: Ensure OpenSSL packages work correctly

### Test Scenarios
1. **HTTPS Connections**: Test SSL/TLS functionality
2. **Certificate Validation**: Test certificate handling
3. **Performance**: Test OpenSSL performance in HTTP context

## 🚨 Critical Notes

1. **Consumer Package**: This consumes OpenSSL, doesn't provide it
2. **Build Artifacts**: Generated files are gitignored
3. **Clean Builds**: Always use separate build directory
4. **Integration Testing**: Primary purpose is testing OpenSSL integration
5. **CMake Integration**: Demonstrates proper CMake + Conan usage

## 📝 Build Troubleshooting

### Common Issues
1. **Generated files in source**: Add to .gitignore and remove from tracking
2. **Build failures**: Clean build directory and retry
3. **Dependency issues**: Check conanfile.txt requirements

### Solutions
```bash
# Remove generated files from git tracking
git rm --cached *.cmake conan*.sh deactivate_*.sh

# Clean build
rm -rf build/ && mkdir build && cd build
conan install .. --output-folder=. --build=missing
cmake .. -DCMAKE_TOOLCHAIN_FILE=conan_toolchain.cmake
```



