---
title: Clearing a Station Tile
---
## Introduction

This documentation provides a guideline on how to clear a station tile in OpenTTD, based on a chat thread.&nbsp;

## The <SwmToken path="/src/station_cmd.cpp" pos="792:2:2" line-data="CommandCost ClearTile_Station(TileIndex tile, DoCommandFlag flags);" repo-id="Z2l0aHViJTNBJTNBT3BlblRURC1jb3BpbG90LWRlbW8lM0ElM0Fzd2ltbWlv" repo-name="OpenTTD-copilot-demo">`ClearTile_Station`</SwmToken> Command

To clear a station tile, you can use the <SwmToken path="/src/station_cmd.cpp" pos="792:2:2" line-data="CommandCost ClearTile_Station(TileIndex tile, DoCommandFlag flags);" repo-id="Z2l0aHViJTNBJTNBT3BlblRURC1jb3BpbG90LWRlbW8lM0ElM0Fzd2ltbWlv" repo-name="OpenTTD-copilot-demo">`ClearTile_Station`</SwmToken> function defined in <SwmPath repo-id="Z2l0aHViJTNBJTNBT3BlblRURC1jb3BpbG90LWRlbW8lM0ElM0Fzd2ltbWlv" repo-name="OpenTTD-copilot-demo" path="/src/station_cmd.cpp">`(OpenTTD-copilot-demo) src/station_cmd.cpp`</SwmPath>.

This function handles the process of clearing a single tile of a station by checking the type of station and ensuring that the appropriate demolition error messages are returned if the station cannot be cleared automatically. Depending on the station type, it calls specific functions to handle the removal process.

## Example

Here is the relevant code excerpt for <SwmToken path="/src/station_cmd.cpp" pos="792:2:2" line-data="CommandCost ClearTile_Station(TileIndex tile, DoCommandFlag flags);" repo-id="Z2l0aHViJTNBJTNBT3BlblRURC1jb3BpbG90LWRlbW8lM0ElM0Fzd2ltbWlv" repo-name="OpenTTD-copilot-demo">`ClearTile_Station`</SwmToken>

<SwmSnippet path="/src/station_cmd.cpp" line="4709" repo-id="Z2l0aHViJTNBJTNBT3BlblRURC1jb3BpbG90LWRlbW8lM0ElM0Fzd2ltbWlv">

---

&nbsp;

```c++
CommandCost ClearTile_Station(TileIndex tile, DoCommandFlag flags)
{
	if (flags & DC_AUTO) {
		switch (GetStationType(tile)) {
			default: break;
			case STATION_RAIL:     return_cmd_error(STR_ERROR_MUST_DEMOLISH_RAILROAD);
			case STATION_WAYPOINT: return_cmd_error(STR_ERROR_BUILDING_MUST_BE_DEMOLISHED);
			case STATION_AIRPORT:  return_cmd_error(STR_ERROR_MUST_DEMOLISH_AIRPORT_FIRST);
			case STATION_TRUCK:    return_cmd_error(HasTileRoadType(tile, RTT_TRAM) ? STR_ERROR_MUST_DEMOLISH_CARGO_TRAM_STATION_FIRST : STR_ERROR_MUST_DEMOLISH_TRUCK_STATION_FIRST);
			case STATION_BUS:      return_cmd_error(HasTileRoadType(tile, RTT_TRAM) ? STR_ERROR_MUST_DEMOLISH_PASSENGER_TRAM_STATION_FIRST : STR_ERROR_MUST_DEMOLISH_BUS_STATION_FIRST);
			case STATION_ROADWAYPOINT: return_cmd_error(STR_ERROR_BUILDING_MUST_BE_DEMOLISHED);
			case STATION_BUOY:     return_cmd_error(STR_ERROR_BUOY_IN_THE_WAY);
			case STATION_DOCK:     return_cmd_error(STR_ERROR_MUST_DEMOLISH_DOCK_FIRST);
			case STATION_OILRIG:
				SetDParam(1, STR_INDUSTRY_NAME_OIL_RIG);
				return_cmd_error(STR_ERROR_GENERIC_OBJECT_IN_THE_WAY);
		}
	}

	switch (GetStationType(tile)) {
		case STATION_RAIL:     return RemoveRailStation(tile, flags);
```

---

</SwmSnippet>

For more details, you can refer to the document, which explains the process of clearing a station tile in the game&nbsp;

<SwmMeta version="3.0.0"><sup>Powered by [Swimm](https://app.swimm.io/)</sup></SwmMeta>
