# Grundlagen

Bevor wir in die GeoStyler Bibliothek einsteigen, werfen wir einen kurzen Blick auf einige grundlegende Voraussetzungen:

Für die Installation von GeoStyler nutzen wir den node package manager ([npm](https://www.npmjs.com/)).
Außerdem verwenden wir für die Entwicklung den JavaScript Standard [EcmaScript 6](https://en.wikipedia.org/wiki/ECMAScript).
Daher empfehlen wir dies auch für die Nutzung unserer Bibliothek.

Da es sich beim GeoStyler um eine React basierte Komponenten Bibliothek handelt, ist es unerlässlich, sich einen
kurzen Überblick über [React](https://reactjs.org/) zu verschaffen.

# GeoStyler Aufbau

Der GeoStyler besteht aus drei wesentlichen Bestandteilen:

1. Die UI - ein Set an grafischen Komponenten zur Nutzerinteraktion
2. Die Style Parser - Übersetzungseinheiten, die zwischen verschiedenen Stilformaten übersetzen
3. Die Data Parser - Übersertzungseinheiten, die zwischen verschiedenen Datenformaten übersetzen

## UI

Die GeoStyler UI Komponenten ermöglichen das Stylen von Geodaten über eine grafische Oberfläche. Es wird
eine Vielzahl von Komponenten angeboten, die sich alle anpassen und anwendungsspezifisch zusammensetzen lassen,
sodass nur die gewünschten Stilelemente editiert werden können.

Das Herzstück der GeoStyler UI ist die `Style` Komponente, auf die später noch weiter eingegangen wird.

## Style Parser

Style Parser ermöglichen das Übersetzen von bestehenden Stilformaten zum internen GeoStyler Stilformat und umgekehrt.
Sie funktionieren wie ein Wörterbuch und erlauben so, dass die GeoStyler UI für viele verschiedene Stilformate genutzt werden kann.
Dazu gehören zur Zeit u.a. SLD, OpenLayers oder auch QML (QGIS Stil).

## Data Parser

Data Parser verhalten sich genauso wie Stilparser, nur dass sie zwischen bestehenden Datenformaten wie SLD oder GeoJSON zum internen
GeoStyler Datenformat übersetzen. Data Parser werden genutzt um attributives Stylen zu ermöglichen. 
