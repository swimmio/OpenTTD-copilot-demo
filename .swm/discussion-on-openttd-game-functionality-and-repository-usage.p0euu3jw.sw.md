---
title: Overview and Station Tile Clearing in OpenTTD Copilot Demo
---
# Overview and Station Tile Clearing in OpenTTD Copilot Demo

## Intro

This document provides an overview of the `swimmio/OpenTTD-copilot-demo` repository and instructions on how to clear a station tile within the game. The information was derived from a chat discussion about the repository.

## Repository Overview

The `swimmio/OpenTTD-copilot-demo` repository is an open-source simulation game based on Transport Tycoon Deluxe. It allows players to build and manage a transportation network, including trains, buses, ships, and airplanes. The game involves planning and constructing infrastructure, managing finances, and optimizing transportation routes to grow a successful transport business.

## Clearing a Station Tile

To clear a station tile in the `OpenTTD` game, follow these steps:

1. Identify the type of station tile you want to clear.
2. Call the appropriate removal function based on the station type:
   - For rail stations, use the `RemoveRailStation` function.
   - For rail waypoints, use the `RemoveRailWaypoint` function.
   - For general station tiles, use the `ClearTile_Station` function.

For more detailed steps, refer to the [clearing-a-station-tile-flow documentation](https://github.com/swimmio/OpenTTD-copilot-demo/blob/9e6a35cbbf18b2558704c7407270e61b3b936ade/.swm/clearing-a-station-tile-flow.iz6bzycy.sw.md#L1-L28).

## Summary

This document provides a brief overview of the `swimmio/OpenTTD-copilot-demo` repository, describing its purpose and functionality. Additionally, it outlines the steps required to clear a station tile within the game, directing users to the appropriate functions and detailed documentation for further guidance.

<SwmMeta version="3.0.0"><sup>Powered by [Swimm](http://localhost:5000/)</sup></SwmMeta>
