# BoundaryFiles

#Dhaka_Zone_pickup is GeoJson file for Dhaka Zones.
#Dhaka_Cluster_Pickup is GeoJson file for Dhaka Clusters.


#Code to make GeoJson
with cte as
(
select name,geom as geom from zones where geo_region_id = 3
)
SELECT 
  OBJECT_CONSTRUCT(
    'type', 'FeatureCollection',
    'features', ARRAY_AGG(
      OBJECT_CONSTRUCT(
        'type', 'Feature',
        'geometry', ST_AsGeoJSON(geom),
        'properties', OBJECT_CONSTRUCT('name', name)
      )
    )
  ) AS geojson
FROM cte;
