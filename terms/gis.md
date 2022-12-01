# Geographic Information System

> Also known as maps, geographics, geospatial

## Definition

In computer science, GIS stands for Geographic Information System. It is a type of system that is designed to store, manipulate, analyze, and visualize geographic data.

## Great references for WYSIWYG

- [Turf.js](https://turfjs.org/)
- [Prosemirror](https://prosemirror.net/)
- [Froala wysiwyg editor](https://froala.com/wysiwyg-editor/)
- [TinyMCE](https://github.com/tinymce/tinymce)
- [Trix Editor](https://trix-editor.org/)

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

```ts
function haversineDistance(
  lat1: number,
  lon1: number,
  lat2: number,
  lon2: number,
  radius: number
): number {
  const deltaLat = lat2 - lat1
  const deltaLon = lon2 - lon1
  const a =
    Math.sin(deltaLat / 2) * Math.sin(deltaLat / 2) +
    Math.cos(lat1) * Math.cos(lat2) *
    Math.sin(deltaLon / 2) * Math.sin(deltaLon / 2)
  const c = 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1 - a))
  const d = radius * c

  return d
}
```

You can use this function like this:

```ts
const lat1 = 51.5074
const lon1 = 0.1278
const lat2 = 40.7128
const lon2 = 74.0060
const radius = 6371 // Earth's radius in kilometers

const distance = haversineDistance(lat1, lon1, lat2, lon2, radius)
```
This will calculate the distance between the two points using the Haversine formula. The distance will be returned in kilometers.