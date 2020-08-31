
# Parsing SLD

In order to parse SLD, we need two things. The `geostyler-sld-parser` and a SLD that we want to parse.

> **info**
> As a reminder: A Styler Parser always translates between a styling format and the internal GeoStyler style format.
> In this case, we will read and write SLD.

We already installed the `geostyler-sld-parser` via

```bash
npm i geostyler-sld-parser
```

in a previous chapter. So now, we just have to import it into our application.

To do so, add following statement to `src/App.js`:

```js
import SldParser from 'geostyler-sld-parser';
```

Next, the SldParser has to be instantiated. This can be done via

```js
const sldParser = new SldParser();
```

In order to read a SLD, the method `readStyle` of the sldParser instance will be used. This method expects
a SLD string as argument and returns a [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) with the matching GeoStyler style.

```js
sldParser.readStyle(sld)
    .then((geostylerStyle) => {
        // Run your actions with the parsed style here, e.g.
        console.log(geostylerStyle);
    });
```

In order to write a SLD, we use the method `writeStyle` of the sldParser instance. This methods expects
a GeoStyler style object as argument and returns a Promise with the matching SLD string.

```js
sldParser.writeStyle(geostylerStyle)
    .then((sld) => {
        // Run your actions with the written style here, e.g.
        console.log(sld);
    });
```

We can manually store an example SLD in a variable or we can dynamically load a SLD available remotely via `fetch()`.
E.g. a [simple point style](https://raw.githubusercontent.com/geostyler/geostyler-sld-parser/master/data/slds/point_simplepoint.sld).

```js
fetch('https://raw.githubusercontent.com/geostyler/geostyler-sld-parser/master/data/slds/point_simplepoint.sld')
    .then((response) => {
        return response.text();
    })
    .then((sld) => {
        // Run your actions with the fetched style here, e.g.
        console.log(sld);
    });
```

Applying this concept to our application, the code should look like below. The variables for the written and read styles were declared
as React-state-variables and we can display their contents in the application.

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

Your application should now look as follows:

[![Read and written SLD](./images/sld-parsed.png)](./images/sld-parsed.png)

The first section shows the original SLD. The second section shows the read SLD in the GeoStyler format. The third section
shows the written SLD.
