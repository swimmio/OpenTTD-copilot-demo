---
title: 'OpenTTD-copilot-demo Repository: Clearing Station Tiles'
---
# OpenTTD-copilot-demo Repository: Clearing Station Tiles

## Introduction

The `swimmio/OpenTTD-copilot-demo` repository is an open-source simulation game based on Transport Tycoon Deluxe. It allows players to build and manage a transportation network, including trains, buses, ships, and airplanes. The game involves planning and constructing infrastructure, managing finances, and optimizing transportation routes to grow a successful transport business.

## Clearing Station Tiles

To clear a station tile in the `OpenTTD` game, you can follow these steps:

1. Identify the type of station tile you want to clear.
2. Call the appropriate removal function based on the station type:
   - For rail stations, use the `RemoveRailStation` function.
   - For rail waypoints, use the `RemoveRailWaypoint` function.
   - For general station tiles, use the `ClearTile_Station` function.

For more detailed steps, refer to the [clearing-a-station-tile-flow documentation](https://github.com/swimmio/OpenTTD-copilot-demo/blob/9e6a35cbbf18b2558704c7407270e61b3b936ade/.swm/clearing-a-station-tile-flow.iz6bzycy.sw.md#L1-L28).

## Code Example

Here is an example of how you can use the `ClearTile_Station` function to clear a station tile in the OpenTTD game:

<SwmSnippet path=".swm/clearing-a-station-tile-flow.iz6bzycy.sw.md" line="1" repo-id="Z2l0aHViJTNBJTNBT3BlblRURC1jb3BpbG90LWRlbW8lM0ElM0Fzd2ltbWlv" repo-name="OpenTTD-copilot-demo">

---

&nbsp;

```c++
#include "station_cmd.h"

// Function to clear a station tile
CommandCost ClearStationTile(TileIndex tile, DoCommandFlag flags) {
    return ClearTile_Station(tile, flags);
}

// Usage example
TileIndex tile_to_clear = ...; // Specify the tile index you want to clear
DoCommandFlag flags = ...; // Specify the appropriate flags

CommandCost result = ClearStationTile(tile_to_clear, flags);
if (result.Failed()) {
    // Handle the error
} else {
    // Tile cleared successfully
}
```

---

</SwmSnippet>

Make sure to include the required headers and set the appropriate values for `tile_to_clear` and `flags`.

## Summary

This document covered the basic functionality for clearing station tiles in the OpenTTD game, including an example code snippet showing how to use the `ClearTile_Station` function. For more details, please refer to the documentation provided in the repository.

<SwmMeta version="3.0.0"><sup>Powered by [Swimm](http://localhost:5000/)</sup></SwmMeta>
