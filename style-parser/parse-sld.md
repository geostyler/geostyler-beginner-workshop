
# SLD parsen

Um SLDs parsen zu können benötigen wir zunächst zwei Dinge. Den `geostyler-sld-parser` und ein SLD, das wir parsen möchten.

> **info**
> Zur Erinnerung: Ein Style Parser übersetzt immer zwischen einem Stilformat und dem internen GeoStyler Stilformat. In diesem
> Fall werden wir ein SLD lesen und schreiben.

Den `geostyler-sld-parser` haben wir bereits mittels

```bash
npm i geostyler-sld-parser
```

in einem vorherigen Kapitel installiert. Daher reicht es jetzt aus, ihn in unsere Applikation zu importieren.

Dazu fügt folgendes Statement der `src/App.js` hinzu:

```js
import SldParser from 'geostyler-sld-parser';
```

Als nächstes muss der SldParser instanziiert werden. Dies geschieht mittels

```js
const sldParser = new SldParser();
```

Um ein SLD zu lesen wird die Funktion `readStyle` der sldParser Instanz genutzt. Diese erwartet einen SLD String
als Argument und gibt ein Promise mit dem entsprechenden GeoStyler Stil zurück.

```js
sldParser.readStyle(sld)
    .then((geostylerStyle) => {
        // Hier Aktionen mit dem gelesenen Stil aufrufen. Bspw.
        console.log(geostylerStyle);
    });
```

Um ein SLD zu schreiben, wird die Funkltion `writeStyle` der sldParser Instanz genutzt. Diese erwartet ein
GeoStyler Style Objekt als Argument und gibt ein Promise mit dem entsprechenden SLD String zurück.

```js
sldParser.writeStyle(geostylerStyle)
    .then((sld) => {
        // Hier Aktionen mit dem geschriebenen Stil aufrufen. Bspw.
        console.log(sld);
    });
```

Ein Beispiel SLD können wir händisch in eine Variable schreiben, oder wir laden uns dynamisch ein online verfügbares SLD
mittels `fetch()` herunter. Bspw. einen [einfachen Punktstil](https://raw.githubusercontent.com/geostyler/geostyler-sld-parser/master/data/slds/point_simplepoint.sld).

```js
fetch('https://raw.githubusercontent.com/geostyler/geostyler-sld-parser/master/data/slds/point_simplepoint.sld')
    .then((response) => {
        return response.text();
    })
    .then((sld) => {
        // Hier Aktionen mit dem geschriebenen Stil aufrufen. Bspw.
        console.log(sld);
    });
```

Auf unsere Applikation angewandt, würde das wie im unteren Code Schnipsel aussehen. Die Variablen für die geschriebenen und gelesenen Stile
haben wir als State-Variablen deklariert und stellen deren Inhalt in der Applikation dar.

```js

import React, { useState, useEffect } from 'react';
import SldParser from 'geostyler-sld-parser';

const sldParser = new SldParser();

function App() {

  const [originalSld, setOriginalSld] = useState('');
  const [sld, setSld] = useState('');
  const [style, setStyle] = useState();

  useEffect(() => {
    fetch('https://raw.githubusercontent.com/geostyler/geostyler-sld-parser/master/data/slds/point_simplepoint.sld')
      .then((res) => {
        if (res.ok) {
          return res.text();
        }
      })
      .then((text) => {
        setOriginalSld(text);
        setSld(text);
      });
  }, []);

  useEffect(() =>  {
    if (!sld) {
      return;
    }

    sldParser.readStyle(sld)
      .then((gsStyle) => {
        setStyle(gsStyle);
      });
  }, [sld]);

  useEffect(() => {
    if (!style) {
      return;
    }

    sldParser.writeStyle(style)
      .then((sldStyle) => {
        setSld(sldStyle);
      });
  }, [style]);

  return (
    <div>
      <p>
        {originalSld}
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

Eure Applikation sollte jetzt folgendermaßen aussehen:

[![Gelesenes und geschriebenes SLD](../images/sld-parsed.png)](../images/sld-parsed.png)

Der erste Abschnitt zeigt das originale SLD, der zweite das gelesene SLD im GeoStyler Stilformat, und der dritte Abschnitt
das geschriebene SLD.