---
title: Testing Framework and Running Tests in the OpenTTD Copilot Demo Repository
---
# Testing Framework and Running Tests in the OpenTTD Copilot Demo Repository

## Introduction

This document provides an overview of the testing framework used in the `swimmio/OpenTTD-copilot-demo` repository and instructions on how to run the tests. The information is derived from the project's repository and chat thread discussions.

## Testing Framework

The repository `swimmio/OpenTTD-copilot-demo` uses the Catch2 framework for testing. This can be identified in multiple files where the following include statement is used:

```cpp
#include "../3rdparty/catch2/catch.hpp"
```

Notable files that include the Catch2 framework are:

- <SwmPath repo-id="Z2l0aHViJTNBJTNBT3BlblRURC1jb3BpbG90LWRlbW8lM0ElM0Fzd2ltbWlv" repo-name="OpenTTD-copilot-demo" path="src/tests/bitmath_func.cpp">`(OpenTTD-copilot-demo) src/tests/bitmath_func.cpp`</SwmPath>
- <SwmPath repo-id="Z2l0aHViJTNBJTNBT3BlblRURC1jb3BpbG90LWRlbW8lM0ElM0Fzd2ltbWlv" repo-name="OpenTTD-copilot-demo" path="src/tests/string_func.cpp">`(OpenTTD-copilot-demo) src/tests/string_func.cpp`</SwmPath>
- <SwmPath repo-id="Z2l0aHViJTNBJTNBT3BlblRURC1jb3BpbG90LWRlbW8lM0ElM0Fzd2ltbWlv" repo-name="OpenTTD-copilot-demo" path="src/tests/test_window_desc.cpp">`(OpenTTD-copilot-demo) src/tests/test_window_desc.cpp`</SwmPath>

Additionally, the <SwmPath repo-id="Z2l0aHViJTNBJTNBT3BlblRURC1jb3BpbG90LWRlbW8lM0ElM0Fzd2ltbWlv" repo-name="OpenTTD-copilot-demo" path="cmake/Catch.cmake">`(OpenTTD-copilot-demo) cmake/Catch.cmake`</SwmPath> file contains CMake commands for configuring Catch2 tests.

## Running Tests

To run tests in the `swimmio/OpenTTD-copilot-demo` repository, follow these steps:

### 1\. Build the Project

Ensure that the project is built using CMake. You can do this with the following commands:

```sh
mkdir build
cd build
cmake ..
make
```

### 2\. Run Tests

Once the project is built, you can run the tests using CTest. In the build directory, execute:

```sh
ctest
```

### 3\. Additional CTest Commands

If you need to discover tests, you can use `catch_discover_tests` in your `CMakeLists.txt` file, which is already set up in the provided <SwmPath repo-id="Z2l0aHViJTNBJTNBT3BlblRURC1jb3BpbG90LWRlbW8lM0ElM0Fzd2ltbWlv" repo-name="OpenTTD-copilot-demo" path="cmake/Catch.cmake">`(OpenTTD-copilot-demo) cmake/Catch.cmake`</SwmPath> file.

For more detailed information, refer to the project’s documentation or the relevant CMake and test files.

## Summary

This document explained the use of the Catch2 testing framework in the `swimmio/OpenTTD-copilot-demo` repository and provided step-by-step instructions on how to build the project and run the tests. For more details, refer to the project’s documentation and CMake files.

<SwmMeta version="3.0.0"><sup>Powered by [Swimm](https://app.swimm.io/)</sup></SwmMeta>
