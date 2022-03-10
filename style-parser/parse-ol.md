
# Parsing an OpenLayers Style

Parsing an OpenLayers style requires the same steps as parsing SLDs.
We will again use the `readStyle` and `writeStyle` methods of the parsers. However, this time, we will use
the `geostyler-openlayers-parser` and do not use an SLD string, but rather an OpenLayers style object.

The installation of the `geostyler-openlayers-parser` was already done in a previous chapter via

```bash
npm i geostyler-openlayers-parser
```

Next, we have to import the parser

```js
import OlParser from 'geostyler-openlayers-parser';
```

and instantiate it.

```js
const olParser = new OlParser();
```

Now, we just need an OpenLayers style that should be parsed

```js
import { Stroke, Fill, Style, Circle } from 'ol/style';

const olStyle = new Style({
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
```

This can now be parsed via `readStyle` and `writeStyle`

```js
olParser.readStyle(olStyle)
    .then((geostylerStyle) => {
        // Run your actions with the read style here, e.g.
        console.log(geostylerStyle.output);
    });

olParser.writeStyle(geostylerStyle)
    .then((olStyle) => {
        // Run your actions with the written style here, e.g.
        console.log(JSON.stringify(olStyle.output));
    });
```

For our application, this should work as follows:

```js
import React, { useState, useEffect } from 'react';
import { Stroke, Fill, Style, Circle } from 'ol/style';

import OlParser from 'geostyler-openlayers-parser';

const olParser = new OlParser();

function App() {

  const originalOlStyle = new Style({
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

  const [olStyle, setOlStyle] = useState(originalOlStyle);
  const [style, setStyle] = useState();

  useEffect(() =>  {
    olParser.readStyle(olStyle)
      .then((gsStyle) => {
        setStyle(gsStyle.output);
      });
  }, [olStyle]);

  useEffect(() => {
    if (!style) {
      return;
    }

    olParser.writeStyle(style)
      .then((newOlStyle) => {
        setOlStyle(newOlStyle.output);
      });
  }, [style]);

  return (
    <div>
      <p>
        {JSON.stringify(originalOlStyle)}
      </p>
      <p>
        {JSON.stringify(style)}
      </p>
      <p>
        {JSON.stringify(olStyle)}
      </p>
    </div>
  );
}

export default App;

```

[![Read and written OpenLayers style](./images/ol-parsed.png)](.images/ol-parsed.png)

The first section shows the original OpenLayers style. The second section shows the parsed OpenLayers style as GeoStyler style. The third
section shows the written OpenLayers style.
