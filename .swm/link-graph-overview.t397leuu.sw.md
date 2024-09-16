---
title: Link Graph Overview
---
```mermaid
graph TD;
 A[InitializeLinkGraphs] --> B[Join Threads];
 B --> C[New Game Starts];
 D[Configure Recalculation Time] --> E[Adjust Based on Map Size];
 E --> F[Manage Performance];
 G[LinkGraphOverlay] --> H[Draw Connections];
 H --> I[Flow of Goods];
 graph TD;
 A[Start] --> B[MultiCommodityFlow::Dijkstra];
 B --> C[Calculate Paths];
 C --> D[MultiCommodityFlow::PushFlow];
 D --> E[Update Flow];
```

# Link Graph Overview

The Link Graph is a key component for managing cargo distribution within the game. It represents the network of connections between different stations and the flow of goods through these connections.

# <SwmToken path="src/linkgraph/linkgraph_gui.h" pos="8:13:13" line-data="/** @file linkgraph_gui.h Declaration of linkgraph overlay GUI. */">`linkgraph`</SwmToken> Class

The <SwmToken path="src/linkgraph/linkgraph_gui.h" pos="8:13:13" line-data="/** @file linkgraph_gui.h Declaration of linkgraph overlay GUI. */">`linkgraph`</SwmToken> class is responsible for handling the creation, merging, and compression of these graphs. It ensures that the cargo distribution network is efficiently managed and updated.

# <SwmToken path="src/linkgraph/mcf.cpp" pos="1:13:15" line-data="/** @file mcf.cpp Definition of Multi-Commodity-Flow solver. */">`Multi-Commodity`</SwmToken> Flow (MCF) Algorithm

The <SwmToken path="src/linkgraph/mcf.cpp" pos="1:13:15" line-data="/** @file mcf.cpp Definition of Multi-Commodity-Flow solver. */">`Multi-Commodity`</SwmToken> Flow (MCF) algorithm is used within the link graph to calculate the optimal flow of goods. This algorithm can be CPU-intensive due to its NP-hard nature.

# Configuration

The recalculation time for the link graph can be configured, allowing for adjustments based on the size of the map and the complexity of the link graph. This helps in managing performance and ensuring timely updates to the flow statistics.

# Visualization

The <SwmToken path="src/linkgraph/linkgraph_gui.h" pos="41:2:2" line-data="class LinkGraphOverlay {">`LinkGraphOverlay`</SwmToken> class is used to visually represent the link graph within the game's interface. It handles drawing the connections and flow of goods between stations.

<SwmSnippet path="/src/linkgraph/linkgraph_gui.h" line="41">

---

The <SwmToken path="src/linkgraph/linkgraph_gui.h" pos="41:2:2" line-data="class LinkGraphOverlay {">`LinkGraphOverlay`</SwmToken> class definition shows how the overlay is created for the specified window, including parameters for the window, widget ID, cargo mask, company mask, and scale.

```c
class LinkGraphOverlay {
public:
	typedef std::map<StationID, LinkProperties> StationLinkMap;
	typedef std::map<StationID, StationLinkMap> LinkMap;
	typedef std::vector<std::pair<StationID, uint> > StationSupplyList;

	static const uint8_t LINK_COLOURS[][12];

	/**
	 * Create a link graph overlay for the specified window.
	 * @param w Window to be drawn into.
	 * @param wid ID of the widget to draw into.
	 * @param cargo_mask Bitmask of cargoes to be shown.
	 * @param company_mask Bitmask of companies to be shown.
	 * @param scale Desired thickness of lines and size of station dots.
	 */
	LinkGraphOverlay(Window *w, WidgetID wid, CargoTypes cargo_mask, CompanyMask company_mask, uint scale) :
			window(w), widget_id(wid), cargo_mask(cargo_mask), company_mask(company_mask), scale(scale), dirty(true)
	{}
```

---

</SwmSnippet>

# Main Functions

There are several main functions in this folder. Some of them are `InitializeLinkGraphs`, <SwmToken path="src/linkgraph/mcf.cpp" pos="1:13:15" line-data="/** @file mcf.cpp Definition of Multi-Commodity-Flow solver. */">`Multi-Commodity`</SwmToken> Flow (MCF) algorithm, <SwmToken path="src/linkgraph/linkgraph_gui.h" pos="8:13:13" line-data="/** @file linkgraph_gui.h Declaration of linkgraph overlay GUI. */">`linkgraph`</SwmToken> class, and <SwmToken path="src/linkgraph/linkgraph_gui.h" pos="41:2:2" line-data="class LinkGraphOverlay {">`LinkGraphOverlay`</SwmToken> class. We will dive a little into `InitializeLinkGraphs` and <SwmToken path="src/linkgraph/mcf.cpp" pos="1:13:15" line-data="/** @file mcf.cpp Definition of Multi-Commodity-Flow solver. */">`Multi-Commodity`</SwmToken> Flow (MCF) algorithm.

## InitializeLinkGraphs

The `InitializeLinkGraphs` function joins all threads related to the link graph, ensuring that any running threads are properly managed when a new game starts.

## <SwmToken path="src/linkgraph/mcf.cpp" pos="1:13:15" line-data="/** @file mcf.cpp Definition of Multi-Commodity-Flow solver. */">`Multi-Commodity`</SwmToken> Flow (MCF) Algorithm

The <SwmToken path="src/linkgraph/mcf.cpp" pos="1:13:15" line-data="/** @file mcf.cpp Definition of Multi-Commodity-Flow solver. */">`Multi-Commodity`</SwmToken> Flow (MCF) algorithm is used within the link graph to calculate the optimal flow of goods. This algorithm can be CPU-intensive due to its NP-hard nature.

# Link Graph Endpoints

Link Graph Endpoints

## <SwmToken path="src/linkgraph/mcf.cpp" pos="257:2:4" line-data="void MultiCommodityFlow::Dijkstra(NodeID source_node, PathVector &amp;paths)">`MultiCommodityFlow::Dijkstra`</SwmToken>

The <SwmToken path="src/linkgraph/mcf.cpp" pos="257:2:4" line-data="void MultiCommodityFlow::Dijkstra(NodeID source_node, PathVector &amp;paths)">`MultiCommodityFlow::Dijkstra`</SwmToken> function is a modified Dijkstra algorithm that grades paths based on a custom annotation. It starts from a source node and calculates paths using the provided annotation and edge iterator.

<SwmSnippet path="/src/linkgraph/mcf.cpp" line="256">

---

The <SwmToken path="src/linkgraph/mcf.cpp" pos="257:2:4" line-data="void MultiCommodityFlow::Dijkstra(NodeID source_node, PathVector &amp;paths)">`MultiCommodityFlow::Dijkstra`</SwmToken> function implementation shows how paths are calculated from a source node using a custom annotation and edge iterator.

```c++
template<class Tannotation, class Tedge_iterator>
void MultiCommodityFlow::Dijkstra(NodeID source_node, PathVector &paths)
{
	typedef std::set<Tannotation *, typename Tannotation::Comparator> AnnoSet;
	Tedge_iterator iter(this->job);
	uint16_t size = this->job.Size();
	AnnoSet annos;
	paths.resize(size, nullptr);
	for (NodeID node = 0; node < size; ++node) {
		Tannotation *anno = new Tannotation(node, node == source_node);
		anno->UpdateAnnotation();
		annos.insert(anno);
		paths[node] = anno;
	}
	while (!annos.empty()) {
		typename AnnoSet::iterator i = annos.begin();
		Tannotation *source = *i;
		annos.erase(i);
		NodeID from = source->GetNode();
		iter.SetNode(source_node, from);
		for (NodeID to = iter.Next(); to != INVALID_NODE; to = iter.Next()) {
```

---

</SwmSnippet>

## <SwmToken path="src/linkgraph/mcf.cpp" pos="344:2:4" line-data="uint MultiCommodityFlow::PushFlow(Node &amp;node, NodeID to, Path *path, uint accuracy,">`MultiCommodityFlow::PushFlow`</SwmToken>

The <SwmToken path="src/linkgraph/mcf.cpp" pos="344:2:4" line-data="uint MultiCommodityFlow::PushFlow(Node &amp;node, NodeID to, Path *path, uint accuracy,">`MultiCommodityFlow::PushFlow`</SwmToken> function pushes flow along a path and updates the unsatisfied demand of the associated edge. It starts from a node and pushes flow to a target node, considering accuracy and maximum saturation.

<SwmSnippet path="/src/linkgraph/mcf.cpp" line="344">

---

The <SwmToken path="src/linkgraph/mcf.cpp" pos="344:2:4" line-data="uint MultiCommodityFlow::PushFlow(Node &amp;node, NodeID to, Path *path, uint accuracy,">`MultiCommodityFlow::PushFlow`</SwmToken> function implementation shows how flow is pushed along a path and the unsatisfied demand of the associated edge is updated.

```c++
uint MultiCommodityFlow::PushFlow(Node &node, NodeID to, Path *path, uint accuracy,
		uint max_saturation)
{
	assert(node.UnsatisfiedDemandTo(to) > 0);
	uint flow = Clamp(node.DemandTo(to) / accuracy, 1, node.UnsatisfiedDemandTo(to));
	flow = path->AddFlow(flow, this->job, max_saturation);
	node.SatisfyDemandTo(to, flow);
	return flow;
}
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBT3BlblRURC1jb3BpbG90LWRlbW8lM0ElM0Fzd2ltbWlv" repo-name="OpenTTD-copilot-demo"><sup>Powered by [Swimm](/)</sup></SwmMeta>
