# WFS parsen

Im Gegensatz zu Style Parsern, können Data Parser Datenformate nur lesen und nicht schreiben. Das bedeutet, dass wir immer
bestehende Datenformate in das GeoStyler Datenformat konvertieren und nicht umgekehrt.

Daher besitzen Data Parser auch nur eine einzelne Funktion - `readData`. Diese Funktion ist für alle Data Parser identisch
und hat als Rückgabewert immer ein GeoStyler Data Objekt.

In diesem Abschnitt zeigen wir, wie man ein WFS parsen kann. Das geparste WFS wird dann im folgenden Kapitel genutzt um
attributives Styling in der UI zu ermöglichen.

Da wir den `geostyler-wfs-parser` bereits durch

```bash
npm i geostyler-wfs-parser
```

installiert haben, müssen wir den Parser nur importieren

```js
import WfsParser from 'geostyler-wfs-parser';
```

und instanziieren.

```js
const wfsParser = new WfsParser();
```

Danach kann ein WFS mittels

```js
wfsParser.readData(wfsParams)
    .then((geostylerData) => {
        // Hier Aktionen mit gelesenem WFS ausführen. Bspw.
        console.log(JSON.stringify(geostylerData));
    });
```

gelesen werden.

Die Variable `wfsParams` ist ein Objekt, welches mindestens url, version, typeName, und srs eines WFS angeben muss.

```js
const wfsParams = {
    url: 'https://ows.terrestris.de/geoserver/terrestris/ows',
    version: '1.1.0',
    typeName: 'terrestris:bundeslaender',
    srsName: 'EPSG:4326'
};
```

In unserer Applikation kann der WFS Data Parser folgendermaßen genutzt werden:

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
    url: 'https://ows.terrestris.de/geoserver/terrestris/ows',
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
        setStyle(geostylerStyle);
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

