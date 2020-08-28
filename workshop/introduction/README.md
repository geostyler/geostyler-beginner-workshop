
---

# Basics

Before diving into the usage of GeoStyler, we will first have a brief look at some prerequirements:

We will be using the node package manager ([npm](https://www.npmjs.com/)) for the installation of GeoStyler.
Furthermore, we will use the JavaScript standard [EcmaScript 6](https://en.wikipedia.org/wiki/ECMAScript) as programming language when developing.
We therefore suggest to do so as well, when using GeoStyler.

Since GeoStyler is a React-based component library, it is crucial to take a look at [React](https://reactjs.org/).

# GeoStyler Architecture

GeoStyler consists of three main building blocks:

1. The UI - a set of ui components to provide user interaction
2. The Style Parsers - translation entities that translate between different styling formats
3. The Data Parsers - translation entites that translate between different data formats

## UI

The GeoStyler UI allows the styling of geographic data via a graphical user interace. We provide a multitude of components, which are customizable and which can be put together to fit many project specific requirements. At the end of the day, you can decide which map elements should be stylable, and which not.

The heart of the GeoStyler UI is the `Style` component, at which we will take a look at a later stage of this workshop.

## Style Parsers

Style Parsers allow translating between different styling formats and the internal GeoStyler styling format. They behave just like dictionaries and by that allow the GeoStyler UI being usable with many different styling formats, like SLD, OpenLayers or QML (the QGIS style), just to name a few.

## Data Parsers

Data Parsers behave just like Style Parsers, with the only difference that they only translate from existing data formats, such as SHP or GeoJSON,
to our internal GeoStyler data format. Data Parsers are being used to enable attributive styling.
