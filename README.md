## oregonhowl-stable-data

This repo is used to keep a collection of semi-static data files for [OregonHOWL](https://oregonhowl.org/).

---

### Data conversion & formatting [scripts](https://github.com/jimmyangel/howl-data)

#### Convert from kml to geojson
```
togeojson HoodNF_OG.kml > HoodNF_OG.json
togeojson SiuslawNF.kml > SiuslawNF.json
togeojson BLM_Forests.kml > BLM_Forests.json
```

#### Extract old growth features
```
mapshaper -i BLM_Forests.json -filter 'name === "2"' -o BLM_Forests_O.json
mapshaper -i SiuslawNF.json -filter 'name === "3"' -o SiuslawNF_O.json
mapshaper -i HoodNF_OG.json -filter 'name === "3"' -o HoodNF_OG_O.json
```

#### Extract tiles
```
mb-util OregonOG.mbtiles oldgrowth
mb-util OregonClearCuts.mbtiles clearcuts
```

#### Ecoregions
```
mapshaper -i or_eco_l3/or_eco_l3.shp -proj wgs84 -simplify 25% -o ecoregions.json
pwildeecomatch.js
sampleterrain for ecoregions.json
```

#### pwilderness
```
mapshaper -i pwilderness/rdls21_albers_OR/rdls21_albers_OR.shp -proj wgs84 -simplify 20% keep-shapes -o pwilderness/rdls21_albers_OR_S.json
```

#### OR-7 shp file
```
change PARAMETER["Central_Parallel" to PARAMETER["latitude_of_origin" in prj file
```

#### MTBS
Use [getMTBS](https://github.com/jimmyangel/getMTBS) utility
```
node node getMTBS.js -y 2017
```

#### BLM shp to geojson
```
Load in mapshaper online
  Then in command line: -proj wgs84
  The export options: "precision=0.0001" - export to geojson
```

#### Forestland
```
mapshaper -i forestland.shp -proj wgs84 -simplify 25% -o forestland.json
```
