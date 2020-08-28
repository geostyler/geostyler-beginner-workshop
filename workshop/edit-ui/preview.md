
# PreviewMap Component

The `PreviewMap` component displays a created style in the map.

In order to to so, the component expects a `style` property that contains the GeoStyler style to display.

To get the style edited in the `Style` component, we use the `onStyleChange` method and store the style
in a state-variable.

```js
import React, { useState } from 'react';
import { Style } from 'geostyler';

import 'antd/dist/antd.css';

function App() {

  const [style, setStyle] = useState();

  return (
    <div>
        <Style
          compact={true}
          onStyleChange={(newStyle) => {setStyle(newStyle)}}
        />
    </div>
  );
}

export default App;
```

Afterwards, we can import the `PreviewMap` component

```js
import { PreviewMap } from 'geostyler';
```

and add it to the application

```js
import React, { useState } from 'react';
import { Style, PreviewMap } from 'geostyler';

import 'antd/dist/antd.css';

function App() {

  const [style, setStyle] = useState();

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

The application should now look like this:


[![PreviewMap Component](./images/previewMap.png)](./images/previewMap.png)
