# Sentry Modifications

This is a fork of [Google Breakpad](https://chromium.googlesource.com/breakpad/breakpad/) maintained by Sentry for use in `sentry-native`.

## Modifications

- **Windows**: Dynamically size minidump paths instead of using `MAX_PATH` constant
- **Windows**: Xbox One build support
- **Linux**: Cast `SIGSTKSZ` to int for compatibility with glibc 2.34+ (where it's no longer a compile-time constant)
- **Build System**: CMake integration (see below)
- **Minimum required C++17**

## Build System Changes

To minimize external dependencies and better integrate with `sentry-native`, this fork uses CMake instead of Breakpad's native Autotools/`configure` build system.

The CMake build files are maintained in the parent `sentry-native` repository:

- `../CMakeLists.txt` - Defines the `breakpad_client` target and lists all source files

The source file list is derived from `breakpad/Makefile.am` but maintained manually in CMake format. When updating this fork, ensure the CMake file list stays in sync with any changes to the build configuration in upstream Breakpad.

### Key Differences from Upstream Build

- **No `configure` script**: The `./configure` file in this directory is unused. It's an artifact from upstream Breakpad.
- **CMake only**: All builds use CMake with explicit source file lists
- **C++17 required**: The CMake build enforces C++17 standard (set in `../CMakeLists.txt`)
- **Client library only**: Only the client library (`breakpad_client`) is built, not the processor tools

## How To Update

1. Merge/rebase from upstream: `https://chromium.googlesource.com/breakpad/breakpad/`
2. Check for changes in `Makefile.am` and update `../CMakeLists.txt` accordingly
3. Review any new platform-specific code that might need adjustments for Xbox or modern glibc
4. Test builds on all supported platforms (Windows, Linux, macOS, Xbox)
