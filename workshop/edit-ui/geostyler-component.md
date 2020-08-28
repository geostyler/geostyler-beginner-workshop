
# GeoStyler Komponente einbinden

Um GeoStyler Komponenten nutzen zu können, müssen diese über das `import` Statement
eingeladen werden. Danach kann die jeweilige Komponente in der Applikation genutzt werden.

```js
import { Komponente } from 'geostyler';

...

return (
    <div>
        <Komponente property1=... />
    </div>
)
```

Grundsätzlich ist es wichtig sich die [Dokumentation](https://geostyler.github.io/geostyler/latest/index.html) der jeweiligen Komponente
anzuschauen und entsprechende Properties zu setzen.

In diesem Kapitel werden wir die `Style` Komponente verwenden. Die entsprechende Dokumentation
befindet sich [hier](https://geostyler.github.io/geostyler/latest/index.html#/Components/Style/Style).

Die `Style` Komponente hat keine verpflichtenden Properties und kann daher ohne weiteres in eine
Applikation eingebunden werden.

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

Anschließend sollte die Style Komponente sichtbar sein und ihr könnt bereits verschiedene Styling Einstellungen vornehmen.

[![Style Komponente](./images/basic.png)](./images/basic.png)

Mit dem `compact` Property können wir das tabellarische Layout der `Style` Komponente verwenden. Dazu muss nur das Property
`compact` auf `true` gesetzt werden.

```js
<Style
  compact={true}
/>
```

Die Applikation sollte jetzt folgendermaßen aussehen:

[![Compact Layout](./images/compact.png)](./images/compact.png)

