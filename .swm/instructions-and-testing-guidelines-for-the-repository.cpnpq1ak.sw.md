---
title: Testing Guidelines and Instructions for the Repo
---
# Testing Guidelines and Instructions for the Repo

## Intro

This document provides an overview of the testing guidelines and instructions for the repository. The information was derived from the project's repository and relevant discussions.

## Testing Framework

This repository uses [Catch2](https://github.com/catchorg/Catch2) for testing. Catch2 is a multi-paradigm test framework for C++.

## Running the Tests

To run the tests, follow these steps:

1. Ensure Catch2 is installed.
2. Compile the source code, including the test files.
3. Execute the compiled test binary.

Example commands:

```sh
mkdir build
cd build
cmake .. -DENABLE_TESTS=ON
make
./test_binary
```

## Test Files

You can find the test cases in the following files:

- [src/tests/test_network_crypto.cpp](https://github.com/swimmio/OpenTTD-copilot-demo/blob/main/src/tests/test_network_crypto.cpp)
- [src/tests/string_func.cpp](https://github.com/swimmio/OpenTTD-copilot-demo/blob/main/src/tests/string_func.cpp)
- [src/tests/bitmath_func.cpp](https://github.com/swimmio/OpenTTD-copilot-demo/blob/main/src/tests/bitmath_func.cpp)
- [src/tests/test_script_admin.cpp](https://github.com/swimmio/OpenTTD-copilot-demo/blob/main/src/tests/test_script_admin.cpp)

## Summary

This document outlines the steps to run the tests in the repository using Catch2, including the commands required to compile and execute the tests. The locations of the test files are also provided for reference.

<SwmMeta version="3.0.0"><sup>Powered by [Swimm](https://app.swimm.io/)</sup></SwmMeta>
