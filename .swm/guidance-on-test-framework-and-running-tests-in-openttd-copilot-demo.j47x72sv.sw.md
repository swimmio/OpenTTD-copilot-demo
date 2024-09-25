---
title: Testing Framework and Execution in OpenTTD-copilot-demo
---
# Testing Framework and Execution in OpenTTD-copilot-demo

## Introduction

This document provides an overview of the test framework used in the `swimmio/OpenTTD-copilot-demo` repository and instructions on how to run the tests.

## Test Framework

The repository uses the Catch2 test framework. This can be identified from several files that include `catch.hpp` from the `3rdparty/catch2` directory, such as:

- [src/tests/bitmath_func.cpp](https://github.com/swimmio/OpenTTD-copilot-demo/blob/9e6a35cbbf18b2558704c7407270e61b3b936ade/src/tests/bitmath_func.cpp)
- [src/tests/string_func.cpp](https://github.com/swimmio/OpenTTD-copilot-demo/blob/9e6a35cbbf18b2558704c7407270e61b3b936ade/src/tests/string_func.cpp)
- [src/tests/test_window_desc.cpp](https://github.com/swimmio/OpenTTD-copilot-demo/blob/9e6a35cbbf18b2558704c7407270e61b3b936ade/src/tests/test_window_desc.cpp)

Additionally, the <SwmPath repo-id="Z2l0aHViJTNBJTNBT3BlblRURC1jb3BpbG90LWRlbW8lM0ElM0Fzd2ltbWlv" repo-name="OpenTTD-copilot-demo" path="cmake/Catch.cmake">`(OpenTTD-copilot-demo) cmake/Catch.cmake`</SwmPath> file describes how to integrate Catch2 tests with CMake.

## Running Tests

To run tests in this repository, follow these steps using the CMake build system:

1. **Configure the project** using CMake to generate the necessary build files.
2. **Build the project** to compile the test executables.
3. **Run the tests** using the compiled test executables.

Here is an example of how you can perform these steps from the command line:

<SwmSnippet path="src/tests/bitmath_func.cpp" line="1" repo-id="Z2l0aHViJTNBJTNBT3BlblRURC1jb3BpbG90LWRlbW8lM0ElM0Fzd2ltbWlv" repo-name="OpenTTD-copilot-demo">

---

&nbsp;

```sh
# Navigate to the root of the repository
cd /path/to/OpenTTD-copilot-demo

# Create and navigate to a build directory
mkdir build && cd build

# Configure the project with CMake
cmake ..

# Build the project
make

# Run the tests
ctest
```

---

</SwmSnippet>

This process assumes you have CMake and a suitable compiler installed on your system. Adjust the commands as needed based on your specific build environment and configuration.

## Summary

The `swimmio/OpenTTD-copilot-demo` repository utilizes the Catch2 test framework, as shown in various test files and the CMake integration file. Follow the provided steps to configure, build, and run the tests using CMake.

<SwmMeta version="3.0.0"><sup>Powered by [Swimm](https://app.swimm.io/)</sup></SwmMeta>
