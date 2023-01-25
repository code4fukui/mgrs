mgrs
====

Utility for converting between WGS84 lat/lng and MGRS coordinates, spunoff from [proj4js](https://github.com/proj4js/proj4js)

has 3 methods

- forward, takes an array of `[lon,lat]` and optional accuracy and returns an mgrs string
- inverse, takes an mgrs string and returns a bbox. 
- toPoint, takes an mgrs string, returns an array of '[lon,lat]'

install dev dependencies with 

```bash
npm install
```

test with

```bash
npm test
```

build with

```bash
npm run build
```

## ES module

```JavaScript
import * as mgrs from "https://code4fukui.github.io/mgrs/mgrs.js";

const mgrsStr = "33UXP04";
const point = mgrs.toPoint(mgrsStr);
console.log(point);
```

## License

Licensed under the MIT license except:

Portions of this software are based on a port of components from the OpenMap
com.bbn.openmap.proj.coords Java package. An initial port was initially created
by Patrice G. Cappelaere and included in Community Mapbuilder
(http://svn.codehaus.org/mapbuilder/), which is licensed under the LGPL license
as per http://www.gnu.org/copyleft/lesser.html. OpenMap is licensed under the
[this license agreement](openmap.md)

# references:
- Wikipedia: https://en.wikipedia.org/wiki/Military_Grid_Reference_System
- GEOTRANS: https://earth-info.nga.mil/#geotrans
