
# Parsing WFS

In contrast to Style Parsers, Data Parsers can only read data formats, not write them. This means, we can only
convert existing data formats into the GeoStyler data format, not the other way around.

Therefore, Data Parses only have one single method - `readData`. This method is the same for all Data Parsers and
always returns a GeoStyler data object.

In this chapter, we will show how to parse WFS. The parsed WFS will then be used in the next chapter to enable
attributive styling in the UI.

Since we already installed the `geostyler-wfs-parser` via

```bash
npm i geostyler-wfs-parser
```

in a previous chapter, we just have to import it via

```js
import WfsParser from 'geostyler-wfs-parser';
```

and instantiate it.

```js
const wfsParser = new WfsParser();
```

Afterwards, a WFS can be read via

```js
wfsParser.readData(wfsParams)
    .then((geostylerData) => {
        // Run your actions with the read WFS here, e.g.
        console.log(JSON.stringify(geostylerData));
    });
```

The variable `wfsParams` expects at least the properties `url`, `version`, `typeName` and `srs` of a WFS.

```js
const wfsParams = {
    url: 'https://ows-demo.terrestris.de/geoserver/terrestris/ows',
    version: '1.1.0',
    typeName: 'terrestris:bundeslaender',
    srsName: 'EPSG:4326'
};
```

In our application, we can use the WFS Data Parser as follows:

```js
import React, { useState, useEffect } from 'react';
import { Stroke, Fill, Style as OlStyle, Circle } from 'ol/style';
import { Style, PreviewMap } from 'geostyler';
import OlParser from 'geostyler-openlayers-parser';
import WfsParser from 'geostyler-wfs-parser';

import 'antd/dist/antd.css';

const olParser = new OlParser();
const wfsParser = new WfsParser();

function App() {

  const wfsParams = {
    url: 'https://ows-demo.terrestris.de/geoserver/terrestris/ows',
    version: '1.1.0',
    typeName: 'terrestris:bundeslaender',
    srsName: 'EPSG:4326'
  };

  const olStyle = new OlStyle({
      stroke: new Stroke({
          color: 'rgba(255, 255, 255, 1.0)',
          width: 1
      }),
      fill: new Fill({
          color: 'rgba(0, 0, 0, 1)'
      }),
      image: new Circle({
          fill: new Fill({
              color: 'rgba(255, 0, 0, 1.0)'
          }),
          radius: 5
      })
  });

  const [style, setStyle] = useState();
  const [data, setData] = useState();

  useEffect(() => {
    olParser.readStyle(olStyle)
      .then((geostylerStyle) => {
        setStyle(geostylerStyle.output);
      });

    wfsParser.readData(wfsParams)
      .then((gsData) => {
        setData(gsData);
      });
  }, []);

  return (
    <div>
        <Style
          style={style}
          compact={true}
          onStyleChange={(newStyle) => {setStyle(newStyle)}}
        />
      {
        style && (
          <PreviewMap
            style={style}
          />
        )
      }
    </div>
  );
}

export default App;
```
