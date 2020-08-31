
# Converting Styles

Since every Style Parser can both read and write, we are also able to convert between different formats.
This can come in very handy if you already have a bunch of styles in a certain styling format, but you now want to use
another styling format.

In this section, we will convert OpenLayers styles to SLD, in order to persist them as files.

In order to convert styles, we have to first read the input style and create thereby a GeoStyler style object. This object can
then be used to convert to the output style format, by using the appropriate Style Parser.

Imagine you want to translate a text from English to French but you only have a `English <-> German` and a `German <-> French` dictionary.
You cannot directly translate from English to French, but you can translate from English to German in a first and from German to French in
a second step. With GeoStyler we do exactly the same. At first, we translate from any input style to the internal GeoStyler format. Then,
we translate from our internal GeoStyler format to any output style. In contrast to translating texts, we do not have to care for grammar,
as can thereby be sure that the translations actually make sense.

Let's import the required parsers

```js
import OlParser from 'geostyler-openlayers-parser';
import SldParser from 'geostyler-sld-parser';
```

and instantiate them

```js
const olParser = new OlParser();
const sldParser = new SldParser();
```

Next, we need an OpenLayers style that we want to convert

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

At first, we read the OpenLayers style with the `geostyler-openlayers-parser` and use the output as argument for the
write method of the `geostyler-sld-parser`.

```js
olParser.readStyle(olStyle)
    .then((geostylerStyle) => {
        return sldParser.writeStyle(geostylerStyle);
    })
    .then((sld) => {
        // Run your actions with the converted style here
        console.log(sld);
    });
```

For our application, it will work as follows:

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

[![To SLD converted OpenLayers style](./images/converted.png)](./images/converted.png)

The first section shows the original OpenLayers style. The second section the parsed OpenLayers style as GeoStyler style. The third section shows
the written SLD style.
