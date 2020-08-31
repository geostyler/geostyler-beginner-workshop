
# Connect Style Parsers with UI

We can connect Style Parsers with the UI in order to display and edit existing styles in the UI.

In this section, we will connect an [OpenLayers style](https://openlayers.org/en/latest/apidoc/module-ol_style_Style-Style.html) with the UI. We will make use of the
`geostyler-openlayers-parser` in order to read the OpenLayers style. The general approach is the same for all parsers.

At first, we have to import the `geostyler-openlayers-parser`

```js
import OlParser from 'geostyler-openlayers-parser';
```

and then instantiate it

```js
const olParser = new OlParser();
```

Then, we need an OpenLayers style object

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

which we then can parse into the GeoStyler style format.

```js
olParser.readStyle(olStyle)
    .then((geostylerStyle) => {
        // Run your actions with the parsed style here
    });
```

In our application we make use of React's state-variables. Please notice the renaming of the OpenLayers class
`Style` to `OlStyle` to avoid naming conflicts with the GeoStyler `Style` component.

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

Afterwards we set the `style` property of the `Style` component to the parsed style.

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

The style defined in the variable `olStyle` will now be displayed directly in the `Style` component of our application, on startup.

[![The OpenLayers style will be displayed directly in the GeoStyler UI.](./images/parser-to-ui.png)](./images/parser-to-ui.png)
