file-drop-zone
[![GitHub release](https://img.shields.io/github/release/PolymerVis/file-drop-zone.svg)](https://github.com/PolymerVis/file-drop-zone/releases)
[![Published on webcomponents.org](https://img.shields.io/badge/webcomponents.org-published-blue.svg)](https://www.webcomponents.org/element/PolymerVis/file-drop-zone)
[![styled with prettier](https://img.shields.io/badge/styled_with-prettier-ff69b4.svg)](https://github.com/prettier/prettier)
==========

<!---
```
<custom-element-demo>
  <template>
    <link rel="import" href="../polymer/lib/elements/dom-bind.html">
    <link rel="import" href="file-drop-zone.html">
    <dom-bind>
      <template is="dom-bind">
        <next-code-block></next-code-block>
      </template>
    </dom-bind>
  </template>
</custom-element-demo>
```
-->

```html
<style>
file-drop-zone {
  border: 1px dashed transparent;
  color: #aaa;
  background-color: #efefef;
  width: 560px;
  height: 300px;
  transition: all .3s;
}
file-drop-zone.dragover {
  border: 1px dashed #E91E63;
  transition: all .3s;
}
file-drop-zone:hover > [slot='drop-zone'],
file-drop-zone.dragover > [slot='drop-zone'] {
  color: #E91E63;
  transition: all .3s;
}
file-drop-zone.errored {
  background-color: #FFEBEE;
  transition: all .3s;
}
file-drop-zone[has-files] {
  color: #2196F3;
  transition: all .3s;
}
[slot='drop-zone'] {
  text-align: center;
  font-size: 1.1em;
  --iron-icon-height: 64px;
  --iron-icon-width: 64px;
}
[slot='drop-zone'] > .title {
  font-size: 1.2em;
}
[slot='drop-zone'] > .small{
  font-size: 0.6em;
}
</style>
<file-drop-zone
  multiple
  accept=".csv, .tsv"
  files="{{files}}"
  last-error="{{error}}"
  on-error="onError">

  <!-- Custom slot element to style the interior of the drop zone -->
  <div slot="drop-zone" class="layout vertical center center-justified">
    <iron-icon icon="description"></iron-icon>
    <div class="title">Drop CSV or TSV files here</div>
    <!-- error message -->
    <div class="small">[[error.message]]</div>
    <!-- list of file selected -->
    <template is="dom-repeat" items="[[files]]">
      <div class="small">[[item.name]]</div>
    </template>
  </div>

</file-drop-zone>
```

`file-drop-zone` is a [Polymer 3.0.0-pre.12](https://www.polymer-project.org/blog/2018-03-23-polymer-3-latest-preview) element for dragging and dropping files into a customizable dropzone. The Polymer 2.0 version can be found in the [master branch](https://github.com/PolymerVis/file-drop-zone).

API documentations and examples can be found at [`file-drop-zone` webcomponents page](https://www.webcomponents.org/element/PolymerVis/file-drop-zone).

## Installation

```
npm install --save @polymer-vis/file-drop-zone
```

## Disclaimers

PolymerVis is a personal project and is NOT in any way affliated with Polymer or Google.

## Quick Start

`file-drop-zone` is a wrapper around an invisible `file` input. The most basic use case is to style the `file-drop-zone` directly, and set the appropriate attributes (`required`, `accept`, `multiple`, `name`) for the `file` input.

```css
file-drop-zone {
  width: 200px;
  height: 200px;
  background-color: #fafafa;
}
```

```html
<file-drop-zone multiple accept="image/*" files="{{files}}"></file-drop-zone>
```

You can also customize the interior of the `file-drop-zone` via `slot` named `drop-zone`.

```html
<file-drop-zone multiple accept="image/*" files="{{files}}">
  <div slot="drop-zone">
    <iron-icon icon="description"></iron-icon>
    <h3>Drop your file here</h3>
  </div>
</file-drop-zone>
```

## Events

#### `change` or `selected`

Fired when one or more files are selected or dropped into the zone.
Return a [FileList](https://developer.mozilla.org/en-US/docs/Web/API/FileList) of selected files.
**Deprecation warning: `selected` event will be deprecated and removed at `2.1.0`. Use `change` event instead.**

#### `error`

Fired when an error is encountered.

## Styling

You can style `file-drop-zone` normally, but there are 3 additional states available for styling.

**.dragover**  
You can style `file-drop-zone` when a file is dragged over the drop-zone with the `dragover` class.

```css
file-drop-zone.dragover {
  border: 1px dashed grey;
}
```

**.errored**  
You can style `file-drop-zone` when there is any error with the `errored` class.

```css
file-drop-zone.errored {
  border: 1px dashed red;
}
```

**[has-files]**  
You can style `file-drop-zone` when there are at least 1 selected file with the `has-files` attribute.

```css
file-drop-zone[has-files] {
  border: 1px solid grey;
}
```
