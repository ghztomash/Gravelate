# Pizza POI files.
POI GPX file of pizza restaurants around Berlin.

Extracted from [Overpass]() with the following query:
```overpass
// define area
(
	area["name"="Berlin"];
	area["name"="Brandenburg"];
)->.searchArea;

// gather results
(
	node["name"~"izza|izze"](area.searchArea);
	node["cuisine"~"pizza"](area.searchArea);
);

// print results
out geom;
```