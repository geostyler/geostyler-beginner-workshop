# OpenLayers Stil parsen

Einen OpenLayers Stil zu parsen erfordert die gleichen Schritte, wie sie auch beim parsen eines SLDs nötig sind.
Wir werden wieder die `readStyle` und `writeStyle` Funktionen des Parsers verwenden. Diesmal machen wir allerdings
vom `geostyler-openlayers-parser` gebrauch und benutzen keinen SLD String, sondern ein OpenLayer Stil Objekt.

Die Installation des `geostyler-openlayers-parser` wurde bereits in einem vorherigen Kapitel mittels

```bash
npm i geostyler-openlayers-parser
```

durchgeführt. Als nächstes muss der Parser durch folgendes Statement importiert werden

```js
import OlParser from 'geostyler-openlayers-parser';
```

und instanziiert werden

```js
const olParser = new OlParser();
```

Jetzt brauchen wir nur noch ein OpenLayers Stil Objekt, das geparsed werden soll

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

Dieses kann jetzt mittels `readStyle` und `writeStyle` geparsed werden

```js
olParser.readStyle(olStyle)
    .then((geostylerStyle) => {
        // Hier Aktionen mit dem gelesenen Stil aufrufen. Bspw.
        console.log(geostylerStyle);
    });

olParser.writeStyle(geostylerStyle)
    .then((olStyle) => {
        // Hier Aktionen mit dem geschriebenen Stil aufrufen. Bspw.
        console.log(JSON.stringify(olStyle));
    });
```

In unserer Applikation sähe das folgendermaßen aus:

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
        setStyle(gsStyle);
      });
  }, [olStyle]);

  useEffect(() => {
    if (!style) {
      return;
    }

    olParser.writeStyle(style)
      .then((newOlStyle) => {
        setOlStyle(newOlStyle);
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

[![Gelesener und geschriebener OpenLayers Stil](../images/ol-parsed.png)](..images/ol-parsed.png)

Der erste Abschnitt zeigt den originalen OpenLayers Stil, der zweite den gelesenen OpenLayers Stil im GeoStyler Stilformat, und der dritte Abschnitt
den geschriebenen OpenLayers Stil.