# Sentry Modifications

This is a fork of [Google Breakpad](https://chromium.googlesource.com/breakpad/breakpad/) maintained by Sentry for use in `sentry-native`.

## Modifications

- **Windows**: Dynamically size minidump paths instead of using `MAX_PATH` constant
- **Windows**: Xbox One build support
- **Linux**: Cast `SIGSTKSZ` to int for compatibility with glibc 2.34+ (where it's no longer a compile-time constant)
- **Build System**: CMake integration (see below)
- **C++17 standard requirement**: upstream uses C++20 (or newer).

## Build System Changes

To minimize external dependencies and better integrate with `sentry-native`, this fork uses CMake instead of Breakpad's native Autotools/`configure` build system.

The CMake build files are maintained in the parent [`sentry-native` repository](https://github.com/getsentry/sentry-native):

- [`../../CMakeLists.txt`](https://github.com/getsentry/sentry-native/blob/master/CMakeLists.txt) - Defines the `breakpad_client` target and lists all source files
