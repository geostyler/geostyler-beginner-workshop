
# Stile konvertieren

Da jeder Style Parser sowohl lesen als auch schreiben kann, können wir auch zwischen verschiedenen Formaten konvertieren.
Das kann sehr nützlich sein, wenn man bspw. bereits eine Reihe von Stilvorschriften in einem Format besitzt, aufgrund technischer
Änderungen mittlerweile aber ein anderes Stilformat unterstützt werden soll.

In diesem Abschnitt werden wir OpenLayers Stile zu SLDs konvertieren, damit wir diese leichter persistieren können.

Um Stile zu konvertieren, muss der Ausgansstil gelesen werden, um ein Objekt im  GeoStyler Stilformat zu erzeugen. Dieses Objekt
wird dann mit dem entsprechenden Style Parser in das Zielformat übersetzt.

Das verhält sich ungefährt so, wie wenn man von Englisch nach Französich übersetzen möchte, allerdings nur ein `Englisch <-> Deutsch`
und ein `Französisch <-> Deutsch` Wörterbuch zur Hand hat. Wir übersetzen also zunächst von Englisch nach Deutsch und dann von Deutsch
nach Französisch. In unserem konkreten Fall also von OpenLayers Stil nach GeoStyler Stil, und dann von GeoStyler Stil nach SLD. Im
Gegensatz zur Sprache macht uns Grammatik keine Probleme und wir können davon ausgehen, dass die Übersetzung stimmt.

Importieren wir zunächst die benötigten Parser

```js
import OlParser from 'geostyler-openlayers-parser';
import SldParser from 'geostyler-sld-parser';
```

und instanziieren sie

```js
const olParser = new OlParser();
const sldParser = new SldParser();
```

Als nächstes benötigen wir ein OpenLayers Stil Objekt das wir konvertieren möchten

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

Um den OpenLayers Stil zu konvertieren, lesen wir diesen zunächst mit dem `geostyler-openlayers-parser` und verwenden dann den Ausgabewert
als Argument für die Schreibfunktion des `geostyler-sld-parser`.

```js
olParser.readStyle(olStyle)
    .then((geostylerStyle) => {
        return sldParser.writeStyle(geostylerStyle);
    })
    .then((sld) => {
        // Hier Aktionen mit dem konvertierten Stil aufrufen. Bspw.
        console.log(sld);
    });
```

Für unsere Applikation sähe das folgendermaßen aus:

```js
import React, { useState, useEffect } from 'react';
import { Stroke, Fill, Style, Circle } from 'ol/style';

import SldParser from 'geostyler-sld-parser';
import OlParser from 'geostyler-openlayers-parser';

const sldParser = new SldParser();
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

  const [sld, setSld] = useState('');
  const [style, setStyle] = useState();

  useEffect(() => {
    olParser.readStyle(originalOlStyle)
      .then((gsStyle) => {
        setStyle(gsStyle);
        return sldParser.writeStyle(gsStyle);
      })
      .then((sldStyle) => {
        setSld(sldStyle);
      });
  }, []);

  return (
    <div>
      <p>
        {JSON.stringify(originalOlStyle)}
      </p>
      <p>
        {JSON.stringify(style)}
      </p>
      <p>
        {sld}
      </p>
    </div>
  );
}

export default App;
```

[![Zu SLD konvertierter OpenLayers Stil](../images/converted.png)](../images/converted.png)

Der erste Abschnitt zeigt den originalen OpenLayers Stil, der zweite den gelesenen OpenLayers Stil im GeoStyler Stilformat, und der dritte Abschnitt
das geschriebenene SLD.