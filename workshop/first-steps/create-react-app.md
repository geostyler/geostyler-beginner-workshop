
# React Applikation erstellen

Wie bereits beschrieben, basiert die GeoStyler UI auf React. Daher sollte zunächst eine
React Applikation erstellt werden, auf deren Grundlage wir dann weiter aufbauen.
Dazu navigiert einfach in einen beliebigen Ordner und führt im Terminal folgenden Befehl aus:

<pre><xmp>npx create-react-app {{ book.reactAppName }}</xmp></pre>

Hierbei entspricht der Name _{{ book.reactAppName }}_ dem Projektnamen und kann beliebig gewählt werden.
Ein entsprechender Ordner sollte im aktuellen Verzeichnis hinzugefügt worden sein. In diesem Ordner wurde
mit Hilfe des Befehls eine einfache React Applikation erstellt, entsprechende Abhängigkeiten installiert
und noch einige praktische Entwicklertools wie hot-reloading hinzugefügt, welche uns die Entwicklung ein
bisschen bequemer machen.

Navigiert nun mit dem Befehl


<pre><xmp>cd {{ book.reactAppName }}</xmp></pre>

in das Projektverzeichnis und startet dort den Entwicklungsserver mittels

<pre><xmp>npm start</xmp></pre>

Die Applikation sollte jetzt über [http://localhost:3000](http://localhost:3000) im Browser erreichbar
und folgendes zu sehen sein:

[![](./images/cra-startpage.png)](./images/cra-startpage.png)

Als nächstes entfernen wir den bestehenden Code, damit wir später mit einer leeren Applikation starten
können. Dazu ersetzt einfach den Inhalt in `src/App.js` mit folgendem Code:

```js
import React from 'react';

function App() {
  return (
    <div></div>
  );
}

export default App;
```

Im nächsten Schritt zeigen wir, wie man GeoStyler installiert.
