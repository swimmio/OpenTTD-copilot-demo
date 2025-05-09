---
title: Overview and Clearing Station Tile in OpenTTD Copilot Demo
---
# Overview and Clearing Station Tile in OpenTTD Copilot Demo

## Introduction

The `swimmio/OpenTTD-copilot-demo` repository is an open-source simulation game derived from Transport Tycoon Deluxe. The primary objective of the game is to manage and optimize a transportation network. This involves building and maintaining infrastructure such as roads, railways, airports, and ports.

## Clearing a Station Tile

To clear a station tile in the `swimmio/OpenTTD-copilot-demo` repository, follow these steps:

1. **Identify the Station Type**: Determine the type of station tile you want to clear (rail, bus, truck, etc.).
2. **Handle Specific Removal Procedures**: Implement the specific removal procedures for the identified station type.
3. **Update Station Information**: Update station-related attributes after removing the tile.

The main function involved is `ClearTile_Station` in the <SwmPath repo-id="Z2l0aHViJTNBJTNBT3BlblRURC1jb3BpbG90LWRlbW8lM0ElM0Fzd2ltbWlv" repo-name="OpenTTD-copilot-demo" path="src/station_cmd.cpp">`(OpenTTD-copilot-demo) src/station_cmd.cpp`</SwmPath> file. This function handles the actual clearing of the station tile based on its type.

For detailed information, you can refer to the [Clearing a Station Tile Flow](https://github.com/swimmio/OpenTTD-copilot-demo/blob/9e6a35cbbf18b2558704c7407270e61b3b936ade/.swm/clearing-a-station-tile-flow.iz6bzycy.sw.md#L1-L28) document.

## Summary

This document provides an overview of the `swimmio/OpenTTD-copilot-demo` repository and instructions on how to clear a station tile. For further details, consult the linked documentation.

<SwmMeta version="3.0.0"><sup>Powered by [Swimm](http://localhost:5000/)</sup></SwmMeta>
