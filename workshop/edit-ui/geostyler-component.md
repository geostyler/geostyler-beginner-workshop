
# Import GeoStyler Component

In order to use GeoStyler components, we have to import these via the `import` statement.
Afterwards, we are able to use the respective component within our application.

```js
import { Component } from 'geostyler';

...

return (
    <div>
        <Component property1=... />
    </div>
)
```

It is very important to take a look at the [Documentation](https://geostyler.github.io/geostyler/latest/index.html) of the used component and
to set the properties accordingly.

We will use the `Style` component in this chapter. The documentation of the component can be
found [here](https://geostyler.github.io/geostyler/latest/index.html#/Components/Style/Style).

The `Style` component does not have any required properties, so we can directly use it in our application.

```js
import React from 'react';
import { Style } from 'geostyler';

import 'antd/dist/antd.css';

function App() {
  return (
    <div>
        <Style />
    </div>
  );
}

export default App;
```

After this, you should be able to see the `Style` component and you should be able to edit styles.

[![Style Component](./images/basic.png)](./images/basic.png)

Through the `compact` property, we are able to use the tabular layout of the `Style` component. To do so, we just have to
set the property `compact` to `true`.

```js
<Style
  compact={true}
/>
```

Your application should now look as follows:

[![Compact Layout](./images/compact.png)](./images/compact.png)
