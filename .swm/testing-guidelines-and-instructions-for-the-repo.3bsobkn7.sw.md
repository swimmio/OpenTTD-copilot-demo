---
title: Testing in the OpenTTD-copilot-demo Repository
---
## Introduction

This document provides instructions on how to test the OpenTTD-copilot-demo repository. The information was derived from a chat thread discussing the testing process and relevant files.

## Testing Framework

The repository uses [Catch2](https://github.com/catchorg/Catch2) for testing. Catch2 is a popular C++ testing framework.

## Testing Instructions

To run the tests, follow these steps:

1. **Ensure Catch2 is installed.**
2. **Compile the source code, including the test files.**
3. **Execute the compiled test binary.**

### Example Commands

```sh
mkdir build
cd build
cmake .. -DENABLE_TESTS=ON
make
./test_binary
```

## Test Files

The test cases are located in several files within the repository. Here are some examples:

- [src/tests/test_network_crypto.cpp](https://github.com/swimmio/OpenTTD-copilot-demo/blob/main/src/tests/test_network_crypto.cpp)
- [src/tests/string_func.cpp](https://github.com/swimmio/OpenTTD-copilot-demo/blob/main/src/tests/string_func.cpp)
- [src/tests/bitmath_func.cpp](https://github.com/swimmio/OpenTTD-copilot-demo/blob/main/src/tests/bitmath_func.cpp)
- [src/tests/test_script_admin.cpp](https://github.com/swimmio/OpenTTD-copilot-demo/blob/main/src/tests/test_script_admin.cpp)

## Summary

This document outlines the process for running tests in the OpenTTD-copilot-demo repository using the Catch2 framework. By following the provided instructions and example commands, you can compile and run the test cases.

<SwmMeta version="3.0.0"><sup>Powered by [Swimm](http://localhost:5000/)</sup></SwmMeta>
