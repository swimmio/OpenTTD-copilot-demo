---
title: Core Networking Components Overview
---
```mermaid
graph TD;
 A[NetworkStartUp] --> B[NetworkCoreInitialize];
 B --> C[Network Available];
 B --> D[Load Windows Socket Library];
 D --> E[WSAStartup];
 E --> F[Network Initialized];
 graph TD;
 A[SendPacket] --> B[Queue Packet];
 B --> C[Send Packet];
 D[ReceivePacket] --> E[Check Connection];
 E --> F[Prepare Packet];
 F --> G[Read Packet Size];
 G --> H[Process Packet Data];
```

# Core Networking Components

Core in Networking refers to the fundamental components and functionalities that are essential for the network operations in <SwmToken path="src/network/core/core.cpp" pos="2:13:13" line-data=" * This file is part of OpenTTD.">`OpenTTD`</SwmToken>. It includes initialization and shutdown processes, various handlers and abstractions, and several macros and headers that are crucial for network operations.

<SwmSnippet path="/src/network/core/core.cpp" line="24">

---

# Network Initialization

The function <SwmToken path="src/network/core/core.cpp" pos="24:2:2" line-data="bool NetworkCoreInitialize()">`NetworkCoreInitialize`</SwmToken> is used to initialize the network core, which is necessary for some platforms. It sets up the network environment, such as loading the Windows socket library on Windows platforms.

```c++
bool NetworkCoreInitialize()
{
/* Let's load the network in windows */
#ifdef _WIN32
	{
		WSADATA wsa;
		Debug(net, 5, "Loading windows socket library");
		if (WSAStartup(MAKEWORD(2, 0), &wsa) != 0) {
			Debug(net, 0, "WSAStartup failed, network unavailable");
			return false;
		}
	}
#endif /* _WIN32 */

	return true;
}
```

---

</SwmSnippet>

<SwmSnippet path="/src/network/network.cpp" line="1290">

---

The function <SwmToken path="src/network/network.cpp" pos="1291:5:5" line-data="	_network_available = NetworkCoreInitialize();">`NetworkCoreInitialize`</SwmToken> is called within <SwmToken path="src/network/network.cpp" pos="1286:2:2" line-data="void NetworkStartUp()">`NetworkStartUp`</SwmToken> to check if the network is available. This ensures that the network core is properly initialized before proceeding with network operations.

```c++
	/* Network is available */
	_network_available = NetworkCoreInitialize();
	_network_dedicated = false;
```

---

</SwmSnippet>

<SwmSnippet path="/src/network/core/core.cpp" line="44">

---

# Network Shutdown

The <SwmToken path="src/network/core/core.cpp" pos="44:2:2" line-data="void NetworkCoreShutdown()">`NetworkCoreShutdown`</SwmToken> function handles the cleanup of the network core. It includes platform-specific code, such as cleaning up the Windows socket library on Windows systems.

```c++
void NetworkCoreShutdown()
{
#if defined(_WIN32)
	WSACleanup();
#endif
}
```

---

</SwmSnippet>

<SwmSnippet path="/src/network/core/core.h" line="12">

---

# Core Macros

The macro <SwmToken path="src/network/core/core.h" pos="12:3:3" line-data="#ifndef NETWORK_CORE_CORE_H">`NETWORK_CORE_CORE_H`</SwmToken> is defined to prevent multiple inclusions of the core header file. This is essential for maintaining the integrity of the core network functionalities.

```c
#ifndef NETWORK_CORE_CORE_H
#define NETWORK_CORE_CORE_H

#include "../../newgrf_config.h"
```

---

</SwmSnippet>

<SwmSnippet path="/src/network/core/packet.h" line="23">

---

# Packet Handling

The <SwmToken path="src/network/core/packet.h" pos="24:11:11" line-data=" * Internal entity of a packet. As everything is sent as a packet,">`packet`</SwmToken> class is an internal entity representing a packet. All network communication involves calling functions that populate the packet. It includes methods for sending and receiving various data types, ensuring data integrity and proper communication.

```c
/**
 * Internal entity of a packet. As everything is sent as a packet,
 * all network communication will need to call the functions that
 * populate the packet.
 * Every packet can be at most a limited number bytes set in the
 * constructor. Overflowing this limit will give an assertion when
 * sending (i.e. writing) the packet. Reading past the size of the
 * packet when receiving will return all 0 values and "" in case of
 * the string.
 *
 * --- Points of attention ---
 *  - all > 1 byte integral values are written in little endian,
 *    unless specified otherwise.
 *      Thus, 0x01234567 would be sent as {0x67, 0x45, 0x23, 0x01}.
 *  - all sent strings are of variable length and terminated by a '\0'.
 *      Thus, the length of the strings is not sent.
 *  - years that are leap years in the 'days since X' to 'date' calculations:
 *     (year % 4 == 0) and ((year % 100 != 0) or (year % 400 == 0))
 */
struct Packet {
	static constexpr size_t EncodedLengthOfPacketSize() { return sizeof(PacketSize); }
```

---

</SwmSnippet>

# Core Endpoints

Core endpoints are essential for sending and receiving packets. They ensure that data is properly transmitted and received over the network.

<SwmSnippet path="/src/network/core/tcp.cpp" line="62">

---

## <SwmToken path="src/network/core/tcp.cpp" pos="68:4:4" line-data="void NetworkTCPSocketHandler::SendPacket(std::unique_ptr&lt;Packet&gt; &amp;&amp;packet)">`SendPacket`</SwmToken>

The <SwmToken path="src/network/core/tcp.cpp" pos="68:4:4" line-data="void NetworkTCPSocketHandler::SendPacket(std::unique_ptr&lt;Packet&gt; &amp;&amp;packet)">`SendPacket`</SwmToken> function places a packet in the <SwmToken path="src/network/core/tcp.cpp" pos="63:17:19" line-data=" * This function puts the packet in the send-queue and it is send as">`send-queue`</SwmToken> and sends it as soon as possible. This function ensures that the packet is prepared for sending and then adds it to the queue.

```c++
/**
 * This function puts the packet in the send-queue and it is send as
 * soon as possible. This is the next tick, or maybe one tick later
 * if the OS-network-buffer is full)
 * @param packet the packet to send
 */
void NetworkTCPSocketHandler::SendPacket(std::unique_ptr<Packet> &&packet)
{
	assert(packet != nullptr);

	packet->PrepareToSend();
	this->packet_queue.push_back(std::move(packet));
}
```

---

</SwmSnippet>

<SwmSnippet path="/src/network/core/tcp.cpp" line="125">

---

## <SwmToken path="src/network/core/tcp.cpp" pos="129:9:9" line-data="std::unique_ptr&lt;Packet&gt; NetworkTCPSocketHandler::ReceivePacket()">`ReceivePacket`</SwmToken>

The <SwmToken path="src/network/core/tcp.cpp" pos="129:9:9" line-data="std::unique_ptr&lt;Packet&gt; NetworkTCPSocketHandler::ReceivePacket()">`ReceivePacket`</SwmToken> function handles receiving a packet for a given client. It checks if the connection is valid, prepares a packet for receiving, reads the packet size, and processes the packet data.

```c++
/**
 * Receives a packet for the given client
 * @return The received packet (or nullptr when it didn't receive one)
 */
std::unique_ptr<Packet> NetworkTCPSocketHandler::ReceivePacket()
{
	ssize_t res;

	if (!this->IsConnected()) return nullptr;

	if (this->packet_recv == nullptr) {
		this->packet_recv = std::make_unique<Packet>(this, TCP_MTU);
	}

	Packet &p = *this->packet_recv.get();

	/* Read packet size */
	if (!p.HasPacketSizeData()) {
		while (p.RemainingBytesToTransfer() != 0) {
			res = p.TransferIn<int>(recv, this->sock, 0);
			if (res == -1) {
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBT3BlblRURC1jb3BpbG90LWRlbW8lM0ElM0Fzd2ltbWlv" repo-name="OpenTTD-copilot-demo"><sup>Powered by [Swimm](/)</sup></SwmMeta>
