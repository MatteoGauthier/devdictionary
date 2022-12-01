# Geographic Information System

> Also known as maps, geographics, geospatial

## Definition

In computer science, GIS stands for Geographic Information System. It is a type of system that is designed to store, manipulate, analyze, and visualize geographic data.

## Great references for WYSIWYG

- [Turf.js](https://turfjs.org/)
- [Mapbox](https://www.mapbox.com/)
- [ToGeoJson - Convert KML, GPX, and TCX to GeoJSON](https://github.com/placemark/togeojson#readme)

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
