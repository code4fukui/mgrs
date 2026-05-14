# mgrs

[
![npm version](https://badge.fury.io/js/mgrs.svg)
](https://badge.fury.io/js/mgrs)
[
![Build Status](https://travis-ci.org/proj4js/mgrs.svg?branch=master)
](https://travis-ci.org/proj4js/mgrs)

> 日本語のREADMEはこちらです: [README.ja.md](README.ja.md)

A utility for converting between WGS84 latitude/longitude and MGRS coordinates, spun off from [proj4js](https://github.com/proj4js/proj4js).

## Installation

Install the package from npm:

```bash
npm install mgrs
```

## Usage

### Node.js (CommonJS)

```javascript
const mgrs = require('mgrs');

const mgrsString = '33UXP04';
const point = mgrs.toPoint(mgrsString);
console.log(point);
//=> [ 16.414501..., 48.249492... ]

const bbox = mgrs.inverse(mgrsString);
console.log(bbox);
//=> [ 16.35842, 48.20443, 16.4705, 48.29443 ] (approx.)
```

### ES Module

You can import the module directly from a CDN:

```javascript
import * as mgrs from "https://code4fukui.github.io/mgrs/mgrs.js";

const mgrsStr = "33UXP04";
const point = mgrs.toPoint(mgrsStr);
console.log(point);
```

## API

### `mgrs.forward(coordinates, [accuracy])`

Converts a WGS84 coordinate to an MGRS string.

-   `coordinates` `<Array<number>>`: An array of `[longitude, latitude]`.
-   `accuracy` `<number>` (optional): The desired precision of the MGRS string. `5` for 1m (default), `4` for 10m, `3` for 100m, `2` for 1km, `1` for 10km.
-   **Returns** `<string>`: The MGRS string.

```javascript
const point = [16.4145, 48.2495];
const mgrsString = mgrs.forward(point, 5);
//=> '33UXP0500444997'
```

### `mgrs.inverse(mgrsString)`

Converts an MGRS string to a WGS84 bounding box.

-   `mgrsString` `<string>`: The MGRS string.
-   **Returns** `<Array<number>>`: A bounding box array `[left, bottom, right, top]` (or `[minLon, minLat, maxLon, maxLat]`).

```javascript
const bbox = mgrs.inverse('33UXP04');
//=> [ 16.358..., 48.204..., 16.470..., 48.294... ]
```

### `mgrs.toPoint(mgrsString)`

Converts an MGRS string to a WGS84 point, representing the center of the MGRS grid square.

-   `mgrsString` `<string>`: The MGRS string.
-   **Returns** `<Array<number>>`: The center point as `[longitude, latitude]`.

```javascript
const point = mgrs.toPoint('33UXP04');
//=> [ 16.41450..., 48.24949... ]
```

## Development

To work on this project locally, clone the repository and install the development dependencies:

```bash
npm install
```

### Testing

Run the test suite:

```bash
npm test
```

### Building

Build the distributable files:

```bash
npm run build
```

## References

-   Wikipedia: [Military Grid Reference System](https://en.wikipedia.org/wiki/Military_Grid_Reference_System)
-   GEOTRANS: [Geographic Translator](https://earth-info.nga.mil/#geotrans)

## License

Licensed under the MIT license except:

Portions of this software are based on a port of components from the OpenMap com.bbn.openmap.proj.coords Java package. An initial port was initially created by Patrice G. Cappelaere and included in Community Mapbuilder (http://svn.codehaus.org/mapbuilder/), which is licensed under the LGPL license as per http://www.gnu.org/copyleft/lesser.html. OpenMap is licensed under [this license agreement](openmap.md).