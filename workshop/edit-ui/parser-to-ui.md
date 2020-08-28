
# Style Parser mit UI verknüpfen

Parser können mit der UI verknüpft werden um bspw. bestehende Stile direkt in der UI anzeigen und editieren zu können.

In diesem Abschnitt werden wir einen OpenLayers Stil mit der UI verknüpfen. Dazu verwenden wir wieder den
`geostyler-openlayers-parser` um den OpenLayers Stil zu lesen. Grundsätzlich ist die Vorgehensweise für alle Parser
identisch.

Zuerst muss der `geostyler-openlayers-parser` importiert werden

```js
import OlParser from 'geostyler-openlayers-parser';
```

und dann instanziiert werden

```js
const olParser = new OlParser();
```

Dann benötigen wir ein OpenLayers Stil Objekt

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

und parsen dieses Objekt in das GeoStyler Stilformat.

```js
olParser.readStyle(olStyle)
    .then((geostylerStyle) => {
        // Hier Aktion mit gelesenem OpenLayers Stil ausführen
    });
```

In unserer Applikation verwenden wir dazu State-Variablen. Achtet hierbei auf die Umbenennung
der OpenLayers `Style` Klasse zu `OlStyle` um Namenskonflikte mit der GeoStyler `Style` Komponente zu vermeiden.

```js
import React, { useState, useEffect } from 'react';
import { Stroke, Fill, Style as OlStyle, Circle } from 'ol/style';
import { Style, PreviewMap } from 'geostyler';
import OlParser from 'geostyler-openlayers-parser';

import 'antd/dist/antd.css';

const olParser = new OlParser();

function App() {

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

  useEffect(() => {
    olParser.readStyle(olStyle)
      .then((geostylerStyle) => {
        setStyle(geostylerStyle);
      });
  }, []);

  return (
    <div>
        <Style
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

Anschließend setzen wir das `style` Property der `Style` Komponente auf den gelesenen Stil.

```js
import React, { useState, useEffect } from 'react';
import { Stroke, Fill, Style as OlStyle, Circle } from 'ol/style';
import { Style, PreviewMap } from 'geostyler';
import OlParser from 'geostyler-openlayers-parser';

import 'antd/dist/antd.css';

const olParser = new OlParser();

function App() {

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

  useEffect(() => {
    olParser.readStyle(olStyle)
      .then((geostylerStyle) => {
        setStyle(geostylerStyle);
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

Der in der Variablen `olStyle` definierte Stil wird jetzt direkt beim Aufruf der Applikation in der `Style` Komponente dargestellt.

[![Der OpenLayers Stil wird direkt in der GeoStyler UI dargestellt](./images/parser-to-ui.png)](./images/parser-to-ui.png)
