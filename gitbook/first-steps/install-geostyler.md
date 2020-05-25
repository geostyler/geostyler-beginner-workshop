# GeoStyler installieren

## GeoStyler UI installieren
Da wir npm nutzen, ist die Installation von GeoStyler sehr einfach.
Öffnet einen Terminal und führt folgenden Befehl im Projektverzeichnis aus:

<pre><xmp>npm i geostyler</xmp></pre>

Zusätzlich werden noch einige weitere Abhängigkeiten benötigt, die auf gleiche Weise
installiert werden können:

<pre><xmp>npm i ol@6 antd@3</xmp></pre>

Hierbei werden [OpenLayers](https://openlayers.org/) in Version 6 und [antd](https://ant.design/) in Version 3 installiert. OpenLayers wird für
die Darstellung von (Vorschau-)Karten benötigt und antd versorgt uns mit grundlegenden UI Komponenten
wie z.B. Buttons.

## GeoStyler Parser installieren

Style und Data Parser müssen separat installiert werden, damit nur die Parser vorhanden sind, die auch gebraucht werden. In diesem Workshop
nutzen wir den SLD und OpenLayers Style Parser, sowie den WFS Data Parser.

Führt folgende Befehle aus um die Parser zu installieren:

<pre><xmp>npm i geostyler-sld-parser</xmp></pre>
<pre><xmp>npm i geostyler-openlayers-parser</xmp></pre>
<pre><xmp>npm i geostyler-wfs-parser</xmp></pre>
