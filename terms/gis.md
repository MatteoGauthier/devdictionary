# Geographic Information System

> Also known as maps, geographics, geospatial

## Definition

In computer science, GIS stands for Geographic Information System. It is a type of system that is designed to store, manipulate, analyze, and visualize geographic data.

## Great references for GIS

- [Turf.js](https://turfjs.org/)
- [Mapbox](https://www.mapbox.com/)
- [ToGeoJson - Convert KML, GPX, and TCX to GeoJSON](https://github.com/placemark/togeojson#readme)

## Map Tiles Provider 

- [Mapbox](https://{s}.tiles.mapbox.com/v4/{mapId}/{z}/{x}/{y}{r}.png?access_token={accessToken})
- [OpenStreetMap](https://{s}.tile.openstreetmap.org/{x}/{y}/{z}.png)

<details>
    <summary>ChatGPT response</summary>
    There are several services that offer hosting of map tiles. Some popular options include:

Mapbox: Mapbox is a platform for designing and publishing custom maps. It offers hosting of map tiles through its Mapbox Studio service, which allows you to design and publish your own custom map styles using a variety of data sources.

Google Maps Platform: Google Maps Platform is a suite of APIs and tools for building location-based applications. It offers hosting of map tiles through its Maps JavaScript API, which allows you to display interactive maps on your website or application.

Bing Maps: Bing Maps is a mapping service provided by Microsoft. It offers hosting of map tiles through its Bing Maps API, which allows you to display maps on your website or application.

HERE Maps: HERE Maps is a mapping service provided by HERE Technologies. It offers hosting of map tiles through its HERE Maps API, which allows you to display maps on your website or application.

MapTiler: MapTiler is a mapping platform that offers hosting of map tiles through its MapTiler Cloud service. This service allows you to store and serve map tiles from MapTiler's globally distributed network of data centers.

It's worth noting that these map tile hosting services may have different pricing structures and features, so it's a good idea to compare them to find the one that best meets your needs.

---

Mattèo Gauthier
Can you show me the URL to get raster image tiles for each
The URL for accessing raster image tiles will depend on the map tile hosting service that you are using. Here are some examples of URLs for accessing raster image tiles from some popular map tile hosting services:

Mapbox: Mapbox uses the following URL pattern to access raster image tiles:
<https://{s}.tiles.mapbox.com/v4/{mapId}/{z}/{x}/{y}{r}.png?access_token={accessToken>}

In this pattern, {s} is a subdomain, {mapId} is the ID of the map style, {z} is the zoom level, {x} and {y} are the x and y tile coordinates, {r} is an optional parameter for retina displays, and {accessToken} is your access token.

Google Maps Platform: Google Maps Platform uses the following URL pattern to access raster image tiles:
<https://www.google.com/maps/@?api=1&map_action=map&center={lat},{lng}&zoom={z>}

In this pattern, {lat} and {lng} are the latitude and longitude of the map center, and {z} is the zoom level.

Bing Maps: Bing Maps uses the following URL pattern to access raster image tiles:
<https://t{s}.tiles.virtualearth.net/tiles/r{quadkey}.jpeg?g=1039>

In this pattern, {s} is a subdomain, and {quadkey} is a string that represents the tile coordinates.

HERE Maps: HERE Maps uses the following URL pattern to access raster image tiles:
<https://{s}.base.maps.cit.api.here.com/maptile/2.1/maptile/newest/normal.day/{z}/{x}/{y}/256/png8?app_id={appId}&app_code={appCode>}

In this pattern, {s} is a subdomain, {z} is the zoom level, {x} and {y} are the x and y tile coordinates, {appId} is your application ID, and {appCode} is your application code.

MapTiler: MapTiler uses the following URL pattern to access raster image tiles:
<https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png>

In this pattern, {s} is a subdomain, {z} is the zoom level, and {x} and {y} are the x and y tile coordinates.

It's worth noting that these URL patterns are just examples, and the actual URLs for accessing raster image tiles may vary depending on the specific map tile hosting service that you are using.
</details>

## Useful snippets

- [Calculate the distance between two geographic position](#calculate-the-distance-between-two-geographic-position)

### Calculate the distance between two geographic position

To calculate the distance between two geographic positions, you can use the Haversine formula. This formula takes into account the curvature of the Earth, so it is well-suited for calculating distances between two points on the surface of the Earth.

Here is the formula for the Haversine distance between two points on a sphere with radius r:

```text
a = sin²(Δφ/2) + cos(φ1)⋅cos(φ2)⋅sin²(Δλ/2)
c = 2⋅atan2(√a, √(1−a))
d = r⋅c
```

where φ1 and φ2 are the latitude of the two points, Δφ is the difference in latitude between the two points, Δλ is the difference in longitude between the two points, a is the square of half the chord length between the two points, c is the great circle distance between the two points, and d is the distance between the two points.

To use this formula, you will need to know the latitude and longitude of the two points, as well as the radius of the Earth. You can then plug these values into the formula to calculate the distance between the two points.

Implementation in Typescript

```js
const getHaversineDistance = (first, second) => {
  const toRadian = (angle) => (Math.PI / 180) * angle
  const RADIUS_OF_EARTH_IN_KM = 6371

  const dLat = (Math.PI / 180) * (second.latitude - first.latitude)
  const dLon = (Math.PI / 180) * (second.longitude - first.longitude)

  // Haversine Formula
  const a =
    Math.pow(Math.sin(dLat / 2), 2) +
    Math.pow(Math.sin(dLon / 2), 2) * Math.cos(toRadian(first.latitude)) * Math.cos(toRadian(second.latitude))
  const c = 2 * Math.asin(Math.sqrt(a))

  return RADIUS_OF_EARTH_IN_KM * c
}
```

You can use this function like this:

```js
const parisCoords = {
  latitude: 48.856613,
  longitude: 2.352222,
}

// Define a set of coordinates to test
const testCoords = {
  latitude: 44.849144,
  longitude: -0.560627,
}

console.log(getHaversineDistance(parisCoords, testCoords))
```

This will calculate the distance between the two points using the Haversine formula. The distance will be returned in kilometers.

### Check if a geographic position is inside a radius from another geographic position

Yes, you can use the Haversine formula to create a geospatial filter that will return coordinates that are within a certain distance (in this case, 5km) from a specific location (in this case, Paris). Here is an example of how you could implement this in JavaScript:

```js
const getHaversineDistance = (first, second) => {
  const toRadian = (angle) => (Math.PI / 180) * angle
  const RADIUS_OF_EARTH_IN_KM = 6371

  const dLat = (Math.PI / 180) * (second.latitude - first.latitude)
  const dLon = (Math.PI / 180) * (second.longitude - first.longitude)

  // Haversine Formula
  const a =
    Math.pow(Math.sin(dLat / 2), 2) +
    Math.pow(Math.sin(dLon / 2), 2) * Math.cos(toRadian(first.latitude)) * Math.cos(toRadian(second.latitude))
  const c = 2 * Math.asin(Math.sqrt(a))

  return RADIUS_OF_EARTH_IN_KM * c
}

const isWithinRadius = (point, center, radius) => {
  return getHaversineDistance(point, center) <= radius
}

const parisCoords = {
  latitude: 48.856613,
  longitude: 2.352222,
}

// Define a set of coordinates to test
const testCoords = {
  latitude: 44.849144,
  longitude: -0.560627,
}

console.log(getHaversineDistance(parisCoords, testCoords))
console.log(isWithinRadius(parisCoords, testCoords, 500))
```

This code uses the Haversine formula to calculate the distance between two sets of coordinates (in this case, the given coordinates and Paris) in kilometers. It then compares the calculated distance to the maximum distance, and returns true if the distance is less than or equal to the maximum distance, and false otherwise. You can adjust the maxDistance variable to change the maximum distance from Paris, and you can also use different coordinates for Paris by updating the parisCoords variable.
