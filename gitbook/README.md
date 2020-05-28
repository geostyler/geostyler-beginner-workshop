<center><img src="images/geo-styler-logo.jpg" style="width:650px;"/></center>

# _{{ book.workshopName }}_

Herzlich Willkommen beim **{{ book.workshopName }}**. Dieser Workshop soll einen einführenden
Überblick über den GeoStyler als ein webbasiertes Werkzeug zur interaktiven Erstellung von kartographischen Style-Vorschriften für Geodaten geben.

In diesem Workshop werden wir eine einfache Anwendung schreiben, mit der Nutzern das Styling von Geodaten über eine UI ermöglicht wird.

Die fertige Anwendung wird folgendermaßen aussehen:

[![Finale Anwendung](./images/geostyler-workshop.gif)](./images/geostyler-workshop.gif)

> **info**
> Wenn ihr diese Seite auf eurem eigenen Gerät besuchen oder die PDF-Version ausdrucken möchtet,
> dann könnt ihr die Workshop-Materialien [hier]({{ book.workshopDownloadUrl }}) herunterladen.

## Überblick

In diesem Workshop werden wir die drei Kernelemente des GeoStylers kennen lernen. Dabei wird keinerlei Vorwissen zum GeoStyler benötigt.

- [Style Parser](./style-parser/README.md) - Übersetzungseinheiten, die die Benutzung (fast) jeden Stilformats erlauben
- [UI Komponenten](./edit-ui/README.md) - Grafische Komponenten zum Editieren von Stilen
- [Data Parser](./data-parser/README.md) - Übersetzungseinheiten, die das Einbinden von Daten erlauben

Jeder Abschnitt baut auf den vorherigen Abschnitten auf. Dadurch empfiehlt es sich, den Workshop beim ersten Mal von
vorne nach hinten durchzuarbeiten.

## Setup

Die folgenden Anweisungen und Übungen setzen voraus, dass bestimmte Anforderungen an euren Computer
erfüllt sind. Bitte stellt sicher, dass folgende Programme installiert sind:

- Einen geeigneten Text Editor, wie z.B.[Atom](https://atom.io/).
- [NodeJS](https://nodejs.org/en/) in Version 12.

## Autoren

{% for author in book.authors %}

- {{ author.name }} ([{{ author.mail }}](mailto:{{ author.mail }}))
  {% endfor %}
