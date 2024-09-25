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

### 4\. Exmaples

<SwmSnippet path="/src/tests/test_network_crypto.cpp" line="23" repo-id="Z2l0aHViJTNBJTNBT3BlblRURC1jb3BpbG90LWRlbW8lM0ElM0Fzd2ltbWlv">

---

This code snippet defines a <SwmToken path="/src/tests/test_network_crypto.cpp" pos="23:2:2" line-data="class MockNetworkSocketHandler : public NetworkSocketHandler {" repo-id="Z2l0aHViJTNBJTNBT3BlblRURC1jb3BpbG90LWRlbW8lM0ElM0Fzd2ltbWlv" repo-name="OpenTTD-copilot-demo">`MockNetworkSocketHandler`</SwmToken> class that inherits from <SwmToken path="/src/network/core/core.h" pos="43:2:2" line-data="class NetworkSocketHandler {" repo-id="Z2l0aHViJTNBJTNBT3BlblRURC1jb3BpbG90LWRlbW8lM0ElM0Fzd2ltbWlv" repo-name="OpenTTD-copilot-demo">`NetworkSocketHandler`</SwmToken>. It has a constructor that takes two optional unique pointers to `NetworkEncryptionHandler` objects as arguments and moves them into the corresponding member variables. It is used to create a mock network socket handler with customizable encryption handlers for receiving and sending data.

```c++
class MockNetworkSocketHandler : public NetworkSocketHandler {
public:
	MockNetworkSocketHandler(std::unique_ptr<NetworkEncryptionHandler> &&receive = {}, std::unique_ptr<NetworkEncryptionHandler> &&send = {})
	{
		this->receive_encryption_handler = std::move(receive);
		this->send_encryption_handler = std::move(send);
	}
};
```

---

</SwmSnippet>

<SwmSnippet path="/src/tests/test_network_crypto.cpp" line="54" repo-id="Z2l0aHViJTNBJTNBT3BlblRURC1jb3BpbG90LWRlbW8lM0ElM0Fzd2ltbWlv">

---

This code snippet defines a `TestPasswordRequestHandler` class that inherits from `NetworkAuthenticationPasswordRequestHandler`. It has a private member variable `password` of type `std::string`. The class has a constructor that takes a `password` parameter and initializes the `password` member variable. It overrides the `SendResponse` function from the base class, but does not provide an implementation. It also overrides the `AskUserForPassword` function and provides an implementation that replies to the request with the stored `password`.

```c++
class TestPasswordRequestHandler : public NetworkAuthenticationPasswordRequestHandler {
private:
	std::string password;
public:
	TestPasswordRequestHandler(std::string &password) : password(password) {}
	void SendResponse() override {}
	void AskUserForPassword(std::shared_ptr<NetworkAuthenticationPasswordRequest> request) override { request->Reply(this->password); }
};
```

---

</SwmSnippet>

### 5\. Framework limitations

The Catch2 framework does not work with mac M1 chips, please make sure you are using a x86 device

## Summary

This document explained the use of the Catch2 testing framework in the `swimmio/OpenTTD-copilot-demo` repository and provided step-by-step instructions on how to build the project and run the tests. For more details, refer to the project’s documentation and CMake files.

<SwmMeta version="3.0.0"><sup>Powered by [Swimm](https://app.swimm.io/)</sup></SwmMeta>
