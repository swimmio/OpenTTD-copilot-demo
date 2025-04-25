---
title: Overview and Instructions for Clearing Station Tiles in OpenTTD Copilot Demo
---
# Overview and Instructions for Clearing Station Tiles in OpenTTD Copilot Demo

## Introduction

This document provides an overview of the `swimmio/OpenTTD-copilot-demo` repository and detailed instructions on how to clear a station tile within the game. The repository is an open-source simulation game based on Transport Tycoon Deluxe. It primarily uses C++ (85.4%) and includes C (11.3%), CMake, Squirrel, Objective-C++, HTML, and other minor languages. The game simulates transportation networks and logistics, allowing players to develop their own transportation empires.

## Clearing a Station Tile

To clear a station tile in the `swimmio/OpenTTD-copilot-demo` repository, follow these steps:

1. **Identify the Station Type**: Determine the type of station tile to be cleared.
2. **Remove Rail Stations**: If it is a rail station, use the `RemoveRailStation` function located in <SwmPath repo-id="Z2l0aHViJTNBJTNBT3BlblRURC1jb3BpbG90LWRlbW8lM0ElM0Fzd2ltbWlv" repo-name="OpenTTD-copilot-demo" path="src/station_cmd.cpp">`(OpenTTD-copilot-demo) src/station_cmd.cpp`</SwmPath>.
3. **Remove Waypoints**: For rail waypoints, use the `RemoveRailWaypoint` function.
4. **Clear Base Station**: Ensure no vehicles are on the ground and clear the tile with `RemoveFromRailBaseStation`.

You can find a detailed explanation and relevant code in [this document](https://github.com/swimmio/OpenTTD-copilot-demo/blob/9e6a35cbbf18b2558704c7407270e61b3b936ade/.swm/clearing-a-station-tile-flow.iz6bzycy.sw.md).

## Conclusion

This documentation provides essential information for working with the `swimmio/OpenTTD-copilot-demo` repository, specifically focusing on clearing station tiles. For more detailed information, refer to the linked document.

<SwmMeta version="3.0.0"><sup>Powered by [Swimm](http://localhost:5000/)</sup></SwmMeta>
