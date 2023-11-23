# Pizza POI files.
POI GPX file of pizza restaurants around Berlin.
Complimentary italian restaurants (possibly pizza).

Extracted from [Overpass]() with the following query:
```overpass
// define area
(
  area["name"="Berlin"]["ISO3166-2"~"DE"];
  area["name"="Brandenburg"]["ISO3166-2"~"DE"];
)->.searchArea;
// gather results
(
  ((
    nwr["name"~"pizza|Pizza|pizzeria|Pizzeria"](area.searchArea);
    nwr["description"~"pizza|Pizza|pizzeria|Pizzeria"](area.searchArea);
    nwr["cuisine"~"pizza"](area.searchArea);
    nwr["cuisine"~"italian_pizza"](area.searchArea);
  );- 
   (
    nwr["cuisine"~"keba|burger|mexican|sushi|turkish"](area.searchArea);
    nwr["brand"](area.searchArea);
    nwr["highway"](area.searchArea);
   );
  );
);
// print results
out geom center;
```

```overpass
// define area
(
  area["name"="Berlin"]["ISO3166-2"~"DE"];
  area["name"="Brandenburg"]["ISO3166-2"~"DE"];
)->.searchArea;

// gather results
(
  (
	nwr["cuisine"~"italian"](area.searchArea)({{bbox}});
  );- 
   (
    nwr["cuisine"~"keba|burger|mexican|sushi|turkish"](area.searchArea)({{bbox}});
    nwr["brand"](area.searchArea)({{bbox}});
    nwr["highway"](area.searchArea)({{bbox}});
    nwr["name"~"pizza|Pizza|pizzeria|Pizzeria"](area.searchArea)({{bbox}});
    nwr["description"~"pizza|Pizza|pizzeria|Pizzeria"](area.searchArea)({{bbox}});
    nwr["cuisine"~"pizza"](area.searchArea)({{bbox}});
    nwr["cuisine"~"italian_pizza"](area.searchArea)({{bbox}});
   );
);
// print results
out geom center;
```

Thanks to Christoph Melanzane for helping refine the query.