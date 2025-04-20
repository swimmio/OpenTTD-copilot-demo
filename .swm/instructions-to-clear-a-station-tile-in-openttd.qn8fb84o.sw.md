---
title: Clearing a Station Tile in OpenTTD
---
# Clearing a Station Tile in OpenTTD

## Introduction

This document provides a guide on how to clear a Station Tile in the OpenTTD codebase. It includes steps to identify and handle the removal of different types of station tiles, ensuring proper demolition procedures, and updating station attributes after changes.

## Steps to Clear a Station Tile

1. **Identify the type of station tile** that needs to be cleared.
2. **Handle specific removal procedures** based on the type of station (e.g., rail, airport, truck, etc.).
3. Ensure proper demolition error messages are returned if the station cannot be cleared automatically.

## Relevant Code and Functions

### Clear Station Tile Function

<SwmSnippet path=".swm/clearing-a-station-tile-flow.iz6bzycy.sw.md" line="1" repo-id="Z2l0aHViJTNBJTNBT3BlblRURC1jb3BpbG90LWRlbW8lM0ElM0Fzd2ltbWlv" repo-name="OpenTTD-copilot-demo">

---

&nbsp;

```cpp
CommandCost ClearTile_Station(TileIndex tile, DoCommandFlag flags);
```

---

</SwmSnippet>

### Removal Functions for Specific Station Types

- `RemoveRailStation`
- `RemoveRailWaypoint`
- `RemoveFromRailBaseStation`

### Updating Station Attributes After Tile Changes

- `void Station::AfterStationTileSetChange(bool adding, StationType type)`
- `void UpdateStationAcceptance(Station *st, bool show_msg)`

## Source Files and References

For more details, you can check the relevant sections in the source files:

- [Clearing a Station Tile Flow](https://github.com/swimmio/OpenTTD-copilot-demo/blob/9e6a35cbbf18b2558704c7407270e61b3b936ade/.swm/clearing-a-station-tile-flow.iz6bzycy.sw.md)
- [Station Command Source Code](https://github.com/swimmio/OpenTTD-copilot-demo/blob/9e6a35cbbf18b2558704c7407270e61b3b936ade/src/station_cmd.cpp#L704-L799)

## Summary

Clearing a Station Tile in OpenTTD involves identifying the type of station tile, handling specific removal procedures, and updating station attributes after the tile changes. The provided functions and code references are essential for implementing this process correctly.

<SwmMeta version="3.0.0"><sup>Powered by [Swimm](http://localhost:5000/)</sup></SwmMeta>
