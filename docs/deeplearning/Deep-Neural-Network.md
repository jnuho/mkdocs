---
draft: false
date: 2024-05-31
categories:
  - Deep Learning
  - Project
authors:
  - junho
---

<p align="left"><strong>Date:</strong> May 31, 2024<br></p>

# L-layer Deep Neural Network with numpy

<head><meta charset="utf-8"/>
<meta content="width=device-width, initial-scale=1.0" name="viewport"/>
<title>Deep+Neural+Network+-+Application+v8</title><script src="https://cdnjs.cloudflare.com/ajax/libs/require.js/2.1.10/require.min.js"></script>
<style type="text/css">
    pre { line-height: 125%; }
td.linenos .normal { color: inherit; background-color: transparent; padding-left: 5px; padding-right: 5px; }
span.linenos { color: inherit; background-color: transparent; padding-left: 5px; padding-right: 5px; }
td.linenos .special { color: #000000; background-color: #ffffc0; padding-left: 5px; padding-right: 5px; }
span.linenos.special { color: #000000; background-color: #ffffc0; padding-left: 5px; padding-right: 5px; }
.highlight .hll { background-color: var(--jp-cell-editor-active-background) }
.highlight { background: var(--jp-cell-editor-background); color: var(--jp-mirror-editor-variable-color) }
.highlight .c { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment */
.highlight .err { color: var(--jp-mirror-editor-error-color) } /* Error */
.highlight .k { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword */
.highlight .o { color: var(--jp-mirror-editor-operator-color); font-weight: bold } /* Operator */
.highlight .p { color: var(--jp-mirror-editor-punctuation-color) } /* Punctuation */
.highlight .ch { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Hashbang */
.highlight .cm { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Multiline */
.highlight .cp { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Preproc */
.highlight .cpf { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.PreprocFile */
.highlight .c1 { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Single */
.highlight .cs { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Special */
.highlight .kc { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Constant */
.highlight .kd { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Declaration */
.highlight .kn { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Namespace */
.highlight .kp { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Pseudo */
.highlight .kr { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Reserved */
.highlight .kt { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Type */
.highlight .m { color: var(--jp-mirror-editor-number-color) } /* Literal.Number */
.highlight .s { color: var(--jp-mirror-editor-string-color) } /* Literal.String */
.highlight .ow { color: var(--jp-mirror-editor-operator-color); font-weight: bold } /* Operator.Word */
.highlight .pm { color: var(--jp-mirror-editor-punctuation-color) } /* Punctuation.Marker */
.highlight .w { color: var(--jp-mirror-editor-variable-color) } /* Text.Whitespace */
.highlight .mb { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Bin */
.highlight .mf { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Float */
.highlight .mh { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Hex */
.highlight .mi { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Integer */
.highlight .mo { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Oct */
.highlight .sa { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Affix */
.highlight .sb { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Backtick */
.highlight .sc { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Char */
.highlight .dl { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Delimiter */
.highlight .sd { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Doc */
.highlight .s2 { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Double */
.highlight .se { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Escape */
.highlight .sh { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Heredoc */
.highlight .si { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Interpol */
.highlight .sx { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Other */
.highlight .sr { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Regex */
.highlight .s1 { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Single */
.highlight .ss { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Symbol */
.highlight .il { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Integer.Long */
  </style>
<style type="text/css">
/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*
 * Mozilla scrollbar styling
 */

/* use standard opaque scrollbars for most nodes */
[data-jp-theme-scrollbars='true'] {
  scrollbar-color: rgb(var(--jp-scrollbar-thumb-color))
    var(--jp-scrollbar-background-color);
}

/* for code nodes, use a transparent style of scrollbar. These selectors
 * will match lower in the tree, and so will override the above */
[data-jp-theme-scrollbars='true'] .CodeMirror-hscrollbar,
[data-jp-theme-scrollbars='true'] .CodeMirror-vscrollbar {
  scrollbar-color: rgba(var(--jp-scrollbar-thumb-color), 0.5) transparent;
}

/* tiny scrollbar */

.jp-scrollbar-tiny {
  scrollbar-color: rgba(var(--jp-scrollbar-thumb-color), 0.5) transparent;
  scrollbar-width: thin;
}

/* tiny scrollbar */

.jp-scrollbar-tiny::-webkit-scrollbar,
.jp-scrollbar-tiny::-webkit-scrollbar-corner {
  background-color: transparent;
  height: 4px;
  width: 4px;
}

.jp-scrollbar-tiny::-webkit-scrollbar-thumb {
  background: rgba(var(--jp-scrollbar-thumb-color), 0.5);
}

.jp-scrollbar-tiny::-webkit-scrollbar-track:horizontal {
  border-left: 0 solid transparent;
  border-right: 0 solid transparent;
}

.jp-scrollbar-tiny::-webkit-scrollbar-track:vertical {
  border-top: 0 solid transparent;
  border-bottom: 0 solid transparent;
}

/*
 * Lumino
 */

.lm-ScrollBar[data-orientation='horizontal'] {
  min-height: 16px;
  max-height: 16px;
  min-width: 45px;
  border-top: 1px solid #a0a0a0;
}

.lm-ScrollBar[data-orientation='vertical'] {
  min-width: 16px;
  max-width: 16px;
  min-height: 45px;
  border-left: 1px solid #a0a0a0;
}

.lm-ScrollBar-button {
  background-color: #f0f0f0;
  background-position: center center;
  min-height: 15px;
  max-height: 15px;
  min-width: 15px;
  max-width: 15px;
}

.lm-ScrollBar-button:hover {
  background-color: #dadada;
}

.lm-ScrollBar-button.lm-mod-active {
  background-color: #cdcdcd;
}

.lm-ScrollBar-track {
  background: #f0f0f0;
}

.lm-ScrollBar-thumb {
  background: #cdcdcd;
}

.lm-ScrollBar-thumb:hover {
  background: #bababa;
}

.lm-ScrollBar-thumb.lm-mod-active {
  background: #a0a0a0;
}

.lm-ScrollBar[data-orientation='horizontal'] .lm-ScrollBar-thumb {
  height: 100%;
  min-width: 15px;
  border-left: 1px solid #a0a0a0;
  border-right: 1px solid #a0a0a0;
}

.lm-ScrollBar[data-orientation='vertical'] .lm-ScrollBar-thumb {
  width: 100%;
  min-height: 15px;
  border-top: 1px solid #a0a0a0;
  border-bottom: 1px solid #a0a0a0;
}

.lm-ScrollBar[data-orientation='horizontal']
  .lm-ScrollBar-button[data-action='decrement'] {
  background-image: var(--jp-icon-caret-left);
  background-size: 17px;
}

.lm-ScrollBar[data-orientation='horizontal']
  .lm-ScrollBar-button[data-action='increment'] {
  background-image: var(--jp-icon-caret-right);
  background-size: 17px;
}

.lm-ScrollBar[data-orientation='vertical']
  .lm-ScrollBar-button[data-action='decrement'] {
  background-image: var(--jp-icon-caret-up);
  background-size: 17px;
}

.lm-ScrollBar[data-orientation='vertical']
  .lm-ScrollBar-button[data-action='increment'] {
  background-image: var(--jp-icon-caret-down);
  background-size: 17px;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-Widget {
  box-sizing: border-box;
  position: relative;
  overflow: hidden;
}

.lm-Widget.lm-mod-hidden {
  display: none !important;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

.lm-AccordionPanel[data-orientation='horizontal'] > .lm-AccordionPanel-title {
  /* Title is rotated for horizontal accordion panel using CSS */
  display: block;
  transform-origin: top left;
  transform: rotate(-90deg) translate(-100%);
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-CommandPalette {
  display: flex;
  flex-direction: column;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.lm-CommandPalette-search {
  flex: 0 0 auto;
}

.lm-CommandPalette-content {
  flex: 1 1 auto;
  margin: 0;
  padding: 0;
  min-height: 0;
  overflow: auto;
  list-style-type: none;
}

.lm-CommandPalette-header {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}

.lm-CommandPalette-item {
  display: flex;
  flex-direction: row;
}

.lm-CommandPalette-itemIcon {
  flex: 0 0 auto;
}

.lm-CommandPalette-itemContent {
  flex: 1 1 auto;
  overflow: hidden;
}

.lm-CommandPalette-itemShortcut {
  flex: 0 0 auto;
}

.lm-CommandPalette-itemLabel {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}

.lm-close-icon {
  border: 1px solid transparent;
  background-color: transparent;
  position: absolute;
  z-index: 1;
  right: 3%;
  top: 0;
  bottom: 0;
  margin: auto;
  padding: 7px 0;
  display: none;
  vertical-align: middle;
  outline: 0;
  cursor: pointer;
}
.lm-close-icon:after {
  content: 'X';
  display: block;
  width: 15px;
  height: 15px;
  text-align: center;
  color: #000;
  font-weight: normal;
  font-size: 12px;
  cursor: pointer;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-DockPanel {
  z-index: 0;
}

.lm-DockPanel-widget {
  z-index: 0;
}

.lm-DockPanel-tabBar {
  z-index: 1;
}

.lm-DockPanel-handle {
  z-index: 2;
}

.lm-DockPanel-handle.lm-mod-hidden {
  display: none !important;
}

.lm-DockPanel-handle:after {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  content: '';
}

.lm-DockPanel-handle[data-orientation='horizontal'] {
  cursor: ew-resize;
}

.lm-DockPanel-handle[data-orientation='vertical'] {
  cursor: ns-resize;
}

.lm-DockPanel-handle[data-orientation='horizontal']:after {
  left: 50%;
  min-width: 8px;
  transform: translateX(-50%);
}

.lm-DockPanel-handle[data-orientation='vertical']:after {
  top: 50%;
  min-height: 8px;
  transform: translateY(-50%);
}

.lm-DockPanel-overlay {
  z-index: 3;
  box-sizing: border-box;
  pointer-events: none;
}

.lm-DockPanel-overlay.lm-mod-hidden {
  display: none !important;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-Menu {
  z-index: 10000;
  position: absolute;
  white-space: nowrap;
  overflow-x: hidden;
  overflow-y: auto;
  outline: none;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.lm-Menu-content {
  margin: 0;
  padding: 0;
  display: table;
  list-style-type: none;
}

.lm-Menu-item {
  display: table-row;
}

.lm-Menu-item.lm-mod-hidden,
.lm-Menu-item.lm-mod-collapsed {
  display: none !important;
}

.lm-Menu-itemIcon,
.lm-Menu-itemSubmenuIcon {
  display: table-cell;
  text-align: center;
}

.lm-Menu-itemLabel {
  display: table-cell;
  text-align: left;
}

.lm-Menu-itemShortcut {
  display: table-cell;
  text-align: right;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-MenuBar {
  outline: none;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.lm-MenuBar-content {
  margin: 0;
  padding: 0;
  display: flex;
  flex-direction: row;
  list-style-type: none;
}

.lm-MenuBar-item {
  box-sizing: border-box;
}

.lm-MenuBar-itemIcon,
.lm-MenuBar-itemLabel {
  display: inline-block;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-ScrollBar {
  display: flex;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.lm-ScrollBar[data-orientation='horizontal'] {
  flex-direction: row;
}

.lm-ScrollBar[data-orientation='vertical'] {
  flex-direction: column;
}

.lm-ScrollBar-button {
  box-sizing: border-box;
  flex: 0 0 auto;
}

.lm-ScrollBar-track {
  box-sizing: border-box;
  position: relative;
  overflow: hidden;
  flex: 1 1 auto;
}

.lm-ScrollBar-thumb {
  box-sizing: border-box;
  position: absolute;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-SplitPanel-child {
  z-index: 0;
}

.lm-SplitPanel-handle {
  z-index: 1;
}

.lm-SplitPanel-handle.lm-mod-hidden {
  display: none !important;
}

.lm-SplitPanel-handle:after {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  content: '';
}

.lm-SplitPanel[data-orientation='horizontal'] > .lm-SplitPanel-handle {
  cursor: ew-resize;
}

.lm-SplitPanel[data-orientation='vertical'] > .lm-SplitPanel-handle {
  cursor: ns-resize;
}

.lm-SplitPanel[data-orientation='horizontal'] > .lm-SplitPanel-handle:after {
  left: 50%;
  min-width: 8px;
  transform: translateX(-50%);
}

.lm-SplitPanel[data-orientation='vertical'] > .lm-SplitPanel-handle:after {
  top: 50%;
  min-height: 8px;
  transform: translateY(-50%);
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-TabBar {
  display: flex;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.lm-TabBar[data-orientation='horizontal'] {
  flex-direction: row;
  align-items: flex-end;
}

.lm-TabBar[data-orientation='vertical'] {
  flex-direction: column;
  align-items: flex-end;
}

.lm-TabBar-content {
  margin: 0;
  padding: 0;
  display: flex;
  flex: 1 1 auto;
  list-style-type: none;
}

.lm-TabBar[data-orientation='horizontal'] > .lm-TabBar-content {
  flex-direction: row;
}

.lm-TabBar[data-orientation='vertical'] > .lm-TabBar-content {
  flex-direction: column;
}

.lm-TabBar-tab {
  display: flex;
  flex-direction: row;
  box-sizing: border-box;
  overflow: hidden;
  touch-action: none; /* Disable native Drag/Drop */
}

.lm-TabBar-tabIcon,
.lm-TabBar-tabCloseIcon {
  flex: 0 0 auto;
}

.lm-TabBar-tabLabel {
  flex: 1 1 auto;
  overflow: hidden;
  white-space: nowrap;
}

.lm-TabBar-tabInput {
  user-select: all;
  width: 100%;
  box-sizing: border-box;
}

.lm-TabBar-tab.lm-mod-hidden {
  display: none !important;
}

.lm-TabBar-addButton.lm-mod-hidden {
  display: none !important;
}

.lm-TabBar.lm-mod-dragging .lm-TabBar-tab {
  position: relative;
}

.lm-TabBar.lm-mod-dragging[data-orientation='horizontal'] .lm-TabBar-tab {
  left: 0;
  transition: left 150ms ease;
}

.lm-TabBar.lm-mod-dragging[data-orientation='vertical'] .lm-TabBar-tab {
  top: 0;
  transition: top 150ms ease;
}

.lm-TabBar.lm-mod-dragging .lm-TabBar-tab.lm-mod-dragging {
  transition: none;
}

.lm-TabBar-tabLabel .lm-TabBar-tabInput {
  user-select: all;
  width: 100%;
  box-sizing: border-box;
  background: inherit;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-TabPanel-tabBar {
  z-index: 1;
}

.lm-TabPanel-stackedPanel {
  z-index: 0;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-Collapse {
  display: flex;
  flex-direction: column;
  align-items: stretch;
}

.jp-Collapse-header {
  padding: 1px 12px;
  background-color: var(--jp-layout-color1);
  border-bottom: solid var(--jp-border-width) var(--jp-border-color2);
  color: var(--jp-ui-font-color1);
  cursor: pointer;
  display: flex;
  align-items: center;
  font-size: var(--jp-ui-font-size0);
  font-weight: 600;
  text-transform: uppercase;
  user-select: none;
}

.jp-Collapser-icon {
  height: 16px;
}

.jp-Collapse-header-collapsed .jp-Collapser-icon {
  transform: rotate(-90deg);
  margin: auto 0;
}

.jp-Collapser-title {
  line-height: 25px;
}

.jp-Collapse-contents {
  padding: 0 12px;
  background-color: var(--jp-layout-color1);
  color: var(--jp-ui-font-color1);
  overflow: auto;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/* This file was auto-generated by ensureUiComponents() in @jupyterlab/buildutils */

/**
 * (DEPRECATED) Support for consuming icons as CSS background images
 */

/* Icons urls */

:root {
  --jp-icon-add-above: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTQiIGhlaWdodD0iMTQiIHZpZXdCb3g9IjAgMCAxNCAxNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPGcgY2xpcC1wYXRoPSJ1cmwoI2NsaXAwXzEzN18xOTQ5MikiPgo8cGF0aCBjbGFzcz0ianAtaWNvbjMiIGQ9Ik00Ljc1IDQuOTMwNjZINi42MjVWNi44MDU2NkM2LjYyNSA3LjAxMTkxIDYuNzkzNzUgNy4xODA2NiA3IDcuMTgwNjZDNy4yMDYyNSA3LjE4MDY2IDcuMzc1IDcuMDExOTEgNy4zNzUgNi44MDU2NlY0LjkzMDY2SDkuMjVDOS40NTYyNSA0LjkzMDY2IDkuNjI1IDQuNzYxOTEgOS42MjUgNC41NTU2NkM5LjYyNSA0LjM0OTQxIDkuNDU2MjUgNC4xODA2NiA5LjI1IDQuMTgwNjZINy4zNzVWMi4zMDU2NkM3LjM3NSAyLjA5OTQxIDcuMjA2MjUgMS45MzA2NiA3IDEuOTMwNjZDNi43OTM3NSAxLjkzMDY2IDYuNjI1IDIuMDk5NDEgNi42MjUgMi4zMDU2NlY0LjE4MDY2SDQuNzVDNC41NDM3NSA0LjE4MDY2IDQuMzc1IDQuMzQ5NDEgNC4zNzUgNC41NTU2NkM0LjM3NSA0Ljc2MTkxIDQuNTQzNzUgNC45MzA2NiA0Ljc1IDQuOTMwNjZaIiBmaWxsPSIjNjE2MTYxIiBzdHJva2U9IiM2MTYxNjEiIHN0cm9rZS13aWR0aD0iMC43Ii8+CjwvZz4KPHBhdGggY2xhc3M9ImpwLWljb24zIiBmaWxsLXJ1bGU9ImV2ZW5vZGQiIGNsaXAtcnVsZT0iZXZlbm9kZCIgZD0iTTExLjUgOS41VjExLjVMMi41IDExLjVWOS41TDExLjUgOS41Wk0xMiA4QzEyLjU1MjMgOCAxMyA4LjQ0NzcyIDEzIDlWMTJDMTMgMTIuNTUyMyAxMi41NTIzIDEzIDEyIDEzTDIgMTNDMS40NDc3MiAxMyAxIDEyLjU1MjMgMSAxMlY5QzEgOC40NDc3MiAxLjQ0NzcxIDggMiA4TDEyIDhaIiBmaWxsPSIjNjE2MTYxIi8+CjxkZWZzPgo8Y2xpcFBhdGggaWQ9ImNsaXAwXzEzN18xOTQ5MiI+CjxyZWN0IGNsYXNzPSJqcC1pY29uMyIgd2lkdGg9IjYiIGhlaWdodD0iNiIgZmlsbD0id2hpdGUiIHRyYW5zZm9ybT0ibWF0cml4KC0xIDAgMCAxIDEwIDEuNTU1NjYpIi8+CjwvY2xpcFBhdGg+CjwvZGVmcz4KPC9zdmc+Cg==);
  --jp-icon-add-below: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTQiIGhlaWdodD0iMTQiIHZpZXdCb3g9IjAgMCAxNCAxNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPGcgY2xpcC1wYXRoPSJ1cmwoI2NsaXAwXzEzN18xOTQ5OCkiPgo8cGF0aCBjbGFzcz0ianAtaWNvbjMiIGQ9Ik05LjI1IDEwLjA2OTNMNy4zNzUgMTAuMDY5M0w3LjM3NSA4LjE5NDM0QzcuMzc1IDcuOTg4MDkgNy4yMDYyNSA3LjgxOTM0IDcgNy44MTkzNEM2Ljc5Mzc1IDcuODE5MzQgNi42MjUgNy45ODgwOSA2LjYyNSA4LjE5NDM0TDYuNjI1IDEwLjA2OTNMNC43NSAxMC4wNjkzQzQuNTQzNzUgMTAuMDY5MyA0LjM3NSAxMC4yMzgxIDQuMzc1IDEwLjQ0NDNDNC4zNzUgMTAuNjUwNiA0LjU0Mzc1IDEwLjgxOTMgNC43NSAxMC44MTkzTDYuNjI1IDEwLjgxOTNMNi42MjUgMTIuNjk0M0M2LjYyNSAxMi45MDA2IDYuNzkzNzUgMTMuMDY5MyA3IDEzLjA2OTNDNy4yMDYyNSAxMy4wNjkzIDcuMzc1IDEyLjkwMDYgNy4zNzUgMTIuNjk0M0w3LjM3NSAxMC44MTkzTDkuMjUgMTAuODE5M0M5LjQ1NjI1IDEwLjgxOTMgOS42MjUgMTAuNjUwNiA5LjYyNSAxMC40NDQzQzkuNjI1IDEwLjIzODEgOS40NTYyNSAxMC4wNjkzIDkuMjUgMTAuMDY5M1oiIGZpbGw9IiM2MTYxNjEiIHN0cm9rZT0iIzYxNjE2MSIgc3Ryb2tlLXdpZHRoPSIwLjciLz4KPC9nPgo8cGF0aCBjbGFzcz0ianAtaWNvbjMiIGZpbGwtcnVsZT0iZXZlbm9kZCIgY2xpcC1ydWxlPSJldmVub2RkIiBkPSJNMi41IDUuNUwyLjUgMy41TDExLjUgMy41TDExLjUgNS41TDIuNSA1LjVaTTIgN0MxLjQ0NzcyIDcgMSA2LjU1MjI4IDEgNkwxIDNDMSAyLjQ0NzcyIDEuNDQ3NzIgMiAyIDJMMTIgMkMxMi41NTIzIDIgMTMgMi40NDc3MiAxMyAzTDEzIDZDMTMgNi41NTIyOSAxMi41NTIzIDcgMTIgN0wyIDdaIiBmaWxsPSIjNjE2MTYxIi8+CjxkZWZzPgo8Y2xpcFBhdGggaWQ9ImNsaXAwXzEzN18xOTQ5OCI+CjxyZWN0IGNsYXNzPSJqcC1pY29uMyIgd2lkdGg9IjYiIGhlaWdodD0iNiIgZmlsbD0id2hpdGUiIHRyYW5zZm9ybT0ibWF0cml4KDEgMS43NDg0NmUtMDcgMS43NDg0NmUtMDcgLTEgNCAxMy40NDQzKSIvPgo8L2NsaXBQYXRoPgo8L2RlZnM+Cjwvc3ZnPgo=);
  --jp-icon-add: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTE5IDEzaC02djZoLTJ2LTZINXYtMmg2VjVoMnY2aDZ2MnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-bell: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE2IDE2IiB2ZXJzaW9uPSIxLjEiPgogICA8cGF0aCBjbGFzcz0ianAtaWNvbjIganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjMzMzMzMzIgogICAgICBkPSJtOCAwLjI5Yy0xLjQgMC0yLjcgMC43My0zLjYgMS44LTEuMiAxLjUtMS40IDMuNC0xLjUgNS4yLTAuMTggMi4yLTAuNDQgNC0yLjMgNS4zbDAuMjggMS4zaDVjMC4wMjYgMC42NiAwLjMyIDEuMSAwLjcxIDEuNSAwLjg0IDAuNjEgMiAwLjYxIDIuOCAwIDAuNTItMC40IDAuNi0xIDAuNzEtMS41aDVsMC4yOC0xLjNjLTEuOS0wLjk3LTIuMi0zLjMtMi4zLTUuMy0wLjEzLTEuOC0wLjI2LTMuNy0xLjUtNS4yLTAuODUtMS0yLjItMS44LTMuNi0xLjh6bTAgMS40YzAuODggMCAxLjkgMC41NSAyLjUgMS4zIDAuODggMS4xIDEuMSAyLjcgMS4yIDQuNCAwLjEzIDEuNyAwLjIzIDMuNiAxLjMgNS4yaC0xMGMxLjEtMS42IDEuMi0zLjQgMS4zLTUuMiAwLjEzLTEuNyAwLjMtMy4zIDEuMi00LjQgMC41OS0wLjcyIDEuNi0xLjMgMi41LTEuM3ptLTAuNzQgMTJoMS41Yy0wLjAwMTUgMC4yOCAwLjAxNSAwLjc5LTAuNzQgMC43OS0wLjczIDAuMDAxNi0wLjcyLTAuNTMtMC43NC0wLjc5eiIgLz4KPC9zdmc+Cg==);
  --jp-icon-bug-dot: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjQiIGhlaWdodD0iMjQiIHZpZXdCb3g9IjAgMCAyNCAyNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiM2MTYxNjEiPgogICAgICAgIDxwYXRoIGZpbGwtcnVsZT0iZXZlbm9kZCIgY2xpcC1ydWxlPSJldmVub2RkIiBkPSJNMTcuMTkgOEgyMFYxMEgxNy45MUMxNy45NiAxMC4zMyAxOCAxMC42NiAxOCAxMVYxMkgyMFYxNEgxOC41SDE4VjE0LjAyNzVDMTUuNzUgMTQuMjc2MiAxNCAxNi4xODM3IDE0IDE4LjVDMTQgMTkuMjA4IDE0LjE2MzUgMTkuODc3OSAxNC40NTQ5IDIwLjQ3MzlDMTMuNzA2MyAyMC44MTE3IDEyLjg3NTcgMjEgMTIgMjFDOS43OCAyMSA3Ljg1IDE5Ljc5IDYuODEgMThINFYxNkg2LjA5QzYuMDQgMTUuNjcgNiAxNS4zNCA2IDE1VjE0SDRWMTJINlYxMUM2IDEwLjY2IDYuMDQgMTAuMzMgNi4wOSAxMEg0VjhINi44MUM3LjI2IDcuMjIgNy44OCA2LjU1IDguNjIgNi4wNEw3IDQuNDFMOC40MSAzTDEwLjU5IDUuMTdDMTEuMDQgNS4wNiAxMS41MSA1IDEyIDVDMTIuNDkgNSAxMi45NiA1LjA2IDEzLjQyIDUuMTdMMTUuNTkgM0wxNyA0LjQxTDE1LjM3IDYuMDRDMTYuMTIgNi41NSAxNi43NCA3LjIyIDE3LjE5IDhaTTEwIDE2SDE0VjE0SDEwVjE2Wk0xMCAxMkgxNFYxMEgxMFYxMloiIGZpbGw9IiM2MTYxNjEiLz4KICAgICAgICA8cGF0aCBkPSJNMjIgMTguNUMyMiAyMC40MzMgMjAuNDMzIDIyIDE4LjUgMjJDMTYuNTY3IDIyIDE1IDIwLjQzMyAxNSAxOC41QzE1IDE2LjU2NyAxNi41NjcgMTUgMTguNSAxNUMyMC40MzMgMTUgMjIgMTYuNTY3IDIyIDE4LjVaIiBmaWxsPSIjNjE2MTYxIi8+CiAgICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-bug: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIj4KICAgIDxwYXRoIGQ9Ik0yMCA4aC0yLjgxYy0uNDUtLjc4LTEuMDctMS40NS0xLjgyLTEuOTZMMTcgNC40MSAxNS41OSAzbC0yLjE3IDIuMTdDMTIuOTYgNS4wNiAxMi40OSA1IDEyIDVjLS40OSAwLS45Ni4wNi0xLjQxLjE3TDguNDEgMyA3IDQuNDFsMS42MiAxLjYzQzcuODggNi41NSA3LjI2IDcuMjIgNi44MSA4SDR2MmgyLjA5Yy0uMDUuMzMtLjA5LjY2LS4wOSAxdjFINHYyaDJ2MWMwIC4zNC4wNC42Ny4wOSAxSDR2MmgyLjgxYzEuMDQgMS43OSAyLjk3IDMgNS4xOSAzczQuMTUtMS4yMSA1LjE5LTNIMjB2LTJoLTIuMDljLjA1LS4zMy4wOS0uNjYuMDktMXYtMWgydi0yaC0ydi0xYzAtLjM0LS4wNC0uNjctLjA5LTFIMjBWOHptLTYgOGgtNHYtMmg0djJ6bTAtNGgtNHYtMmg0djJ6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-build: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTYiIHZpZXdCb3g9IjAgMCAyNCAyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTE0LjkgMTcuNDVDMTYuMjUgMTcuNDUgMTcuMzUgMTYuMzUgMTcuMzUgMTVDMTcuMzUgMTMuNjUgMTYuMjUgMTIuNTUgMTQuOSAxMi41NUMxMy41NCAxMi41NSAxMi40NSAxMy42NSAxMi40NSAxNUMxMi40NSAxNi4zNSAxMy41NCAxNy40NSAxNC45IDE3LjQ1Wk0yMC4xIDE1LjY4TDIxLjU4IDE2Ljg0QzIxLjcxIDE2Ljk1IDIxLjc1IDE3LjEzIDIxLjY2IDE3LjI5TDIwLjI2IDE5LjcxQzIwLjE3IDE5Ljg2IDIwIDE5LjkyIDE5LjgzIDE5Ljg2TDE4LjA5IDE5LjE2QzE3LjczIDE5LjQ0IDE3LjMzIDE5LjY3IDE2LjkxIDE5Ljg1TDE2LjY0IDIxLjdDMTYuNjIgMjEuODcgMTYuNDcgMjIgMTYuMyAyMkgxMy41QzEzLjMyIDIyIDEzLjE4IDIxLjg3IDEzLjE1IDIxLjdMMTIuODkgMTkuODVDMTIuNDYgMTkuNjcgMTIuMDcgMTkuNDQgMTEuNzEgMTkuMTZMOS45NjAwMiAxOS44NkM5LjgxMDAyIDE5LjkyIDkuNjIwMDIgMTkuODYgOS41NDAwMiAxOS43MUw4LjE0MDAyIDE3LjI5QzguMDUwMDIgMTcuMTMgOC4wOTAwMiAxNi45NSA4LjIyMDAyIDE2Ljg0TDkuNzAwMDIgMTUuNjhMOS42NTAwMSAxNUw5LjcwMDAyIDE0LjMxTDguMjIwMDIgMTMuMTZDOC4wOTAwMiAxMy4wNSA4LjA1MDAyIDEyLjg2IDguMTQwMDIgMTIuNzFMOS41NDAwMiAxMC4yOUM5LjYyMDAyIDEwLjEzIDkuODEwMDIgMTAuMDcgOS45NjAwMiAxMC4xM0wxMS43MSAxMC44NEMxMi4wNyAxMC41NiAxMi40NiAxMC4zMiAxMi44OSAxMC4xNUwxMy4xNSA4LjI4OTk4QzEzLjE4IDguMTI5OTggMTMuMzIgNy45OTk5OCAxMy41IDcuOTk5OThIMTYuM0MxNi40NyA3Ljk5OTk4IDE2LjYyIDguMTI5OTggMTYuNjQgOC4yODk5OEwxNi45MSAxMC4xNUMxNy4zMyAxMC4zMiAxNy43MyAxMC41NiAxOC4wOSAxMC44NEwxOS44MyAxMC4xM0MyMCAxMC4wNyAyMC4xNyAxMC4xMyAyMC4yNiAxMC4yOUwyMS42NiAxMi43MUMyMS43NSAxMi44NiAyMS43MSAxMy4wNSAyMS41OCAxMy4xNkwyMC4xIDE0LjMxTDIwLjE1IDE1TDIwLjEgMTUuNjhaIi8+CiAgICA8cGF0aCBkPSJNNy4zMjk2NiA3LjQ0NDU0QzguMDgzMSA3LjAwOTU0IDguMzM5MzIgNi4wNTMzMiA3LjkwNDMyIDUuMjk5ODhDNy40NjkzMiA0LjU0NjQzIDYuNTA4MSA0LjI4MTU2IDUuNzU0NjYgNC43MTY1NkM1LjM5MTc2IDQuOTI2MDggNS4xMjY5NSA1LjI3MTE4IDUuMDE4NDkgNS42NzU5NEM0LjkxMDA0IDYuMDgwNzEgNC45NjY4MiA2LjUxMTk4IDUuMTc2MzQgNi44NzQ4OEM1LjYxMTM0IDcuNjI4MzIgNi41NzYyMiA3Ljg3OTU0IDcuMzI5NjYgNy40NDQ1NFpNOS42NTcxOCA0Ljc5NTkzTDEwLjg2NzIgNC45NTE3OUMxMC45NjI4IDQuOTc3NDEgMTEuMDQwMiA1LjA3MTMzIDExLjAzODIgNS4xODc5M0wxMS4wMzg4IDYuOTg4OTNDMTEuMDQ1NSA3LjEwMDU0IDEwLjk2MTYgNy4xOTUxOCAxMC44NTUgNy4yMTA1NEw5LjY2MDAxIDcuMzgwODNMOS4yMzkxNSA4LjEzMTg4TDkuNjY5NjEgOS4yNTc0NUM5LjcwNzI5IDkuMzYyNzEgOS42NjkzNCA5LjQ3Njk5IDkuNTc0MDggOS41MzE5OUw4LjAxNTIzIDEwLjQzMkM3LjkxMTMxIDEwLjQ5MiA3Ljc5MzM3IDEwLjQ2NzcgNy43MjEwNSAxMC4zODI0TDYuOTg3NDggOS40MzE4OEw2LjEwOTMxIDkuNDMwODNMNS4zNDcwNCAxMC4zOTA1QzUuMjg5MDkgMTAuNDcwMiA1LjE3MzgzIDEwLjQ5MDUgNS4wNzE4NyAxMC40MzM5TDMuNTEyNDUgOS41MzI5M0MzLjQxMDQ5IDkuNDc2MzMgMy4zNzY0NyA5LjM1NzQxIDMuNDEwNzUgOS4yNTY3OUwzLjg2MzQ3IDguMTQwOTNMMy42MTc0OSA3Ljc3NDg4TDMuNDIzNDcgNy4zNzg4M0wyLjIzMDc1IDcuMjEyOTdDMi4xMjY0NyA3LjE5MjM1IDIuMDQwNDkgNy4xMDM0MiAyLjA0MjQ1IDYuOTg2ODJMMi4wNDE4NyA1LjE4NTgyQzIuMDQzODMgNS4wNjkyMiAyLjExOTA5IDQuOTc5NTggMi4yMTcwNCA0Ljk2OTIyTDMuNDIwNjUgNC43OTM5M0wzLjg2NzQ5IDQuMDI3ODhMMy40MTEwNSAyLjkxNzMxQzMuMzczMzcgMi44MTIwNCAzLjQxMTMxIDIuNjk3NzYgMy41MTUyMyAyLjYzNzc2TDUuMDc0MDggMS43Mzc3NkM1LjE2OTM0IDEuNjgyNzYgNS4yODcyOSAxLjcwNzA0IDUuMzU5NjEgMS43OTIzMUw2LjExOTE1IDIuNzI3ODhMNi45ODAwMSAyLjczODkzTDcuNzI0OTYgMS43ODkyMkM3Ljc5MTU2IDEuNzA0NTggNy45MTU0OCAxLjY3OTIyIDguMDA4NzkgMS43NDA4Mkw5LjU2ODIxIDIuNjQxODJDOS42NzAxNyAyLjY5ODQyIDkuNzEyODUgMi44MTIzNCA5LjY4NzIzIDIuOTA3OTdMOS4yMTcxOCA0LjAzMzgzTDkuNDYzMTYgNC4zOTk4OEw5LjY1NzE4IDQuNzk1OTNaIi8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-caret-down-empty-thin: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwIDIwIj4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSIgc2hhcGUtcmVuZGVyaW5nPSJnZW9tZXRyaWNQcmVjaXNpb24iPgoJCTxwb2x5Z29uIGNsYXNzPSJzdDEiIHBvaW50cz0iOS45LDEzLjYgMy42LDcuNCA0LjQsNi42IDkuOSwxMi4yIDE1LjQsNi43IDE2LjEsNy40ICIvPgoJPC9nPgo8L3N2Zz4K);
  --jp-icon-caret-down-empty: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiIHNoYXBlLXJlbmRlcmluZz0iZ2VvbWV0cmljUHJlY2lzaW9uIj4KICAgIDxwYXRoIGQ9Ik01LjIsNS45TDksOS43bDMuOC0zLjhsMS4yLDEuMmwtNC45LDVsLTQuOS01TDUuMiw1Ljl6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-caret-down: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiIHNoYXBlLXJlbmRlcmluZz0iZ2VvbWV0cmljUHJlY2lzaW9uIj4KICAgIDxwYXRoIGQ9Ik01LjIsNy41TDksMTEuMmwzLjgtMy44SDUuMnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-caret-left: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSIgc2hhcGUtcmVuZGVyaW5nPSJnZW9tZXRyaWNQcmVjaXNpb24iPgoJCTxwYXRoIGQ9Ik0xMC44LDEyLjhMNy4xLDlsMy44LTMuOGwwLDcuNkgxMC44eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-caret-right: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiIHNoYXBlLXJlbmRlcmluZz0iZ2VvbWV0cmljUHJlY2lzaW9uIj4KICAgIDxwYXRoIGQ9Ik03LjIsNS4yTDEwLjksOWwtMy44LDMuOFY1LjJINy4yeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-caret-up-empty-thin: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwIDIwIj4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSIgc2hhcGUtcmVuZGVyaW5nPSJnZW9tZXRyaWNQcmVjaXNpb24iPgoJCTxwb2x5Z29uIGNsYXNzPSJzdDEiIHBvaW50cz0iMTUuNCwxMy4zIDkuOSw3LjcgNC40LDEzLjIgMy42LDEyLjUgOS45LDYuMyAxNi4xLDEyLjYgIi8+Cgk8L2c+Cjwvc3ZnPgo=);
  --jp-icon-caret-up: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSIgc2hhcGUtcmVuZGVyaW5nPSJnZW9tZXRyaWNQcmVjaXNpb24iPgoJCTxwYXRoIGQ9Ik01LjIsMTAuNUw5LDYuOGwzLjgsMy44SDUuMnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-case-sensitive: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwIDIwIj4KICA8ZyBjbGFzcz0ianAtaWNvbjIiIGZpbGw9IiM0MTQxNDEiPgogICAgPHJlY3QgeD0iMiIgeT0iMiIgd2lkdGg9IjE2IiBoZWlnaHQ9IjE2Ii8+CiAgPC9nPgogIDxnIGNsYXNzPSJqcC1pY29uLWFjY2VudDIiIGZpbGw9IiNGRkYiPgogICAgPHBhdGggZD0iTTcuNiw4aDAuOWwzLjUsOGgtMS4xTDEwLDE0SDZsLTAuOSwySDRMNy42LDh6IE04LDkuMUw2LjQsMTNoMy4yTDgsOS4xeiIvPgogICAgPHBhdGggZD0iTTE2LjYsOS44Yy0wLjIsMC4xLTAuNCwwLjEtMC43LDAuMWMtMC4yLDAtMC40LTAuMS0wLjYtMC4yYy0wLjEtMC4xLTAuMi0wLjQtMC4yLTAuNyBjLTAuMywwLjMtMC42LDAuNS0wLjksMC43Yy0wLjMsMC4xLTAuNywwLjItMS4xLDAuMmMtMC4zLDAtMC41LDAtMC43LTAuMWMtMC4yLTAuMS0wLjQtMC4yLTAuNi0wLjNjLTAuMi0wLjEtMC4zLTAuMy0wLjQtMC41IGMtMC4xLTAuMi0wLjEtMC40LTAuMS0wLjdjMC0wLjMsMC4xLTAuNiwwLjItMC44YzAuMS0wLjIsMC4zLTAuNCwwLjQtMC41QzEyLDcsMTIuMiw2LjksMTIuNSw2LjhjMC4yLTAuMSwwLjUtMC4xLDAuNy0wLjIgYzAuMy0wLjEsMC41LTAuMSwwLjctMC4xYzAuMiwwLDAuNC0wLjEsMC42LTAuMWMwLjIsMCwwLjMtMC4xLDAuNC0wLjJjMC4xLTAuMSwwLjItMC4yLDAuMi0wLjRjMC0xLTEuMS0xLTEuMy0xIGMtMC40LDAtMS40LDAtMS40LDEuMmgtMC45YzAtMC40LDAuMS0wLjcsMC4yLTFjMC4xLTAuMiwwLjMtMC40LDAuNS0wLjZjMC4yLTAuMiwwLjUtMC4zLDAuOC0wLjNDMTMuMyw0LDEzLjYsNCwxMy45LDQgYzAuMywwLDAuNSwwLDAuOCwwLjFjMC4zLDAsMC41LDAuMSwwLjcsMC4yYzAuMiwwLjEsMC40LDAuMywwLjUsMC41QzE2LDUsMTYsNS4yLDE2LDUuNnYyLjljMCwwLjIsMCwwLjQsMCwwLjUgYzAsMC4xLDAuMSwwLjIsMC4zLDAuMmMwLjEsMCwwLjIsMCwwLjMsMFY5Ljh6IE0xNS4yLDYuOWMtMS4yLDAuNi0zLjEsMC4yLTMuMSwxLjRjMCwxLjQsMy4xLDEsMy4xLTAuNVY2Ljl6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-check: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIj4KICAgIDxwYXRoIGQ9Ik05IDE2LjE3TDQuODMgMTJsLTEuNDIgMS40MUw5IDE5IDIxIDdsLTEuNDEtMS40MXoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-circle-empty: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEyIDJDNi40NyAyIDIgNi40NyAyIDEyczQuNDcgMTAgMTAgMTAgMTAtNC40NyAxMC0xMFMxNy41MyAyIDEyIDJ6bTAgMThjLTQuNDEgMC04LTMuNTktOC04czMuNTktOCA4LTggOCAzLjU5IDggOC0zLjU5IDgtOCA4eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-circle: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMTggMTgiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPGNpcmNsZSBjeD0iOSIgY3k9IjkiIHI9IjgiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-clear: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8bWFzayBpZD0iZG9udXRIb2xlIj4KICAgIDxyZWN0IHdpZHRoPSIyNCIgaGVpZ2h0PSIyNCIgZmlsbD0id2hpdGUiIC8+CiAgICA8Y2lyY2xlIGN4PSIxMiIgY3k9IjEyIiByPSI4IiBmaWxsPSJibGFjayIvPgogIDwvbWFzaz4KCiAgPGcgY2xhc3M9ImpwLWljb24zIiBmaWxsPSIjNjE2MTYxIj4KICAgIDxyZWN0IGhlaWdodD0iMTgiIHdpZHRoPSIyIiB4PSIxMSIgeT0iMyIgdHJhbnNmb3JtPSJyb3RhdGUoMzE1LCAxMiwgMTIpIi8+CiAgICA8Y2lyY2xlIGN4PSIxMiIgY3k9IjEyIiByPSIxMCIgbWFzaz0idXJsKCNkb251dEhvbGUpIi8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-close: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbi1ub25lIGpwLWljb24tc2VsZWN0YWJsZS1pbnZlcnNlIGpwLWljb24zLWhvdmVyIiBmaWxsPSJub25lIj4KICAgIDxjaXJjbGUgY3g9IjEyIiBjeT0iMTIiIHI9IjExIi8+CiAgPC9nPgoKICA8ZyBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIGpwLWljb24tYWNjZW50Mi1ob3ZlciIgZmlsbD0iIzYxNjE2MSI+CiAgICA8cGF0aCBkPSJNMTkgNi40MUwxNy41OSA1IDEyIDEwLjU5IDYuNDEgNSA1IDYuNDEgMTAuNTkgMTIgNSAxNy41OSA2LjQxIDE5IDEyIDEzLjQxIDE3LjU5IDE5IDE5IDE3LjU5IDEzLjQxIDEyeiIvPgogIDwvZz4KCiAgPGcgY2xhc3M9ImpwLWljb24tbm9uZSBqcC1pY29uLWJ1c3kiIGZpbGw9Im5vbmUiPgogICAgPGNpcmNsZSBjeD0iMTIiIGN5PSIxMiIgcj0iNyIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-code-check: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyNCIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBzaGFwZS1yZW5kZXJpbmc9Imdlb21ldHJpY1ByZWNpc2lvbiI+CiAgICA8cGF0aCBkPSJNNi41OSwzLjQxTDIsOEw2LjU5LDEyLjZMOCwxMS4xOEw0LjgyLDhMOCw0LjgyTDYuNTksMy40MU0xMi40MSwzLjQxTDExLDQuODJMMTQuMTgsOEwxMSwxMS4xOEwxMi40MSwxMi42TDE3LDhMMTIuNDEsMy40MU0yMS41OSwxMS41OUwxMy41LDE5LjY4TDkuODMsMTZMOC40MiwxNy40MUwxMy41LDIyLjVMMjMsMTNMMjEuNTksMTEuNTlaIiAvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-code: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjIiIGhlaWdodD0iMjIiIHZpZXdCb3g9IjAgMCAyOCAyOCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CgkJPHBhdGggZD0iTTExLjQgMTguNkw2LjggMTRMMTEuNCA5LjRMMTAgOEw0IDE0TDEwIDIwTDExLjQgMTguNlpNMTYuNiAxOC42TDIxLjIgMTRMMTYuNiA5LjRMMTggOEwyNCAxNEwxOCAyMEwxNi42IDE4LjZWMTguNloiLz4KCTwvZz4KPC9zdmc+Cg==);
  --jp-icon-collapse-all: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGgKICAgICAgICAgICAgZD0iTTggMmMxIDAgMTEgMCAxMiAwczIgMSAyIDJjMCAxIDAgMTEgMCAxMnMwIDItMiAyQzIwIDE0IDIwIDQgMjAgNFMxMCA0IDYgNGMwLTIgMS0yIDItMnoiIC8+CiAgICAgICAgPHBhdGgKICAgICAgICAgICAgZD0iTTE4IDhjMC0xLTEtMi0yLTJTNSA2IDQgNnMtMiAxLTIgMmMwIDEgMCAxMSAwIDEyczEgMiAyIDJjMSAwIDExIDAgMTIgMHMyLTEgMi0yYzAtMSAwLTExIDAtMTJ6bS0yIDB2MTJINFY4eiIgLz4KICAgICAgICA8cGF0aCBkPSJNNiAxM3YyaDh2LTJ6IiAvPgogICAgPC9nPgo8L3N2Zz4K);
  --jp-icon-console: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwMCAyMDAiPgogIDxnIGNsYXNzPSJqcC1jb25zb2xlLWljb24tYmFja2dyb3VuZC1jb2xvciBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiMwMjg4RDEiPgogICAgPHBhdGggZD0iTTIwIDE5LjhoMTYwdjE1OS45SDIweiIvPgogIDwvZz4KICA8ZyBjbGFzcz0ianAtY29uc29sZS1pY29uLWNvbG9yIGpwLWljb24tc2VsZWN0YWJsZS1pbnZlcnNlIiBmaWxsPSIjZmZmIj4KICAgIDxwYXRoIGQ9Ik0xMDUgMTI3LjNoNDB2MTIuOGgtNDB6TTUxLjEgNzdMNzQgOTkuOWwtMjMuMyAyMy4zIDEwLjUgMTAuNSAyMy4zLTIzLjNMOTUgOTkuOSA4NC41IDg5LjQgNjEuNiA2Ni41eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-copy: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMTggMTgiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTExLjksMUgzLjJDMi40LDEsMS43LDEuNywxLjcsMi41djEwLjJoMS41VjIuNWg4LjdWMXogTTE0LjEsMy45aC04Yy0wLjgsMC0xLjUsMC43LTEuNSwxLjV2MTAuMmMwLDAuOCwwLjcsMS41LDEuNSwxLjVoOCBjMC44LDAsMS41LTAuNywxLjUtMS41VjUuNEMxNS41LDQuNiwxNC45LDMuOSwxNC4xLDMuOXogTTE0LjEsMTUuNWgtOFY1LjRoOFYxNS41eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-copyright: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIGVuYWJsZS1iYWNrZ3JvdW5kPSJuZXcgMCAwIDI0IDI0IiBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCI+CiAgPGcgY2xhc3M9ImpwLWljb24zIiBmaWxsPSIjNjE2MTYxIj4KICAgIDxwYXRoIGQ9Ik0xMS44OCw5LjE0YzEuMjgsMC4wNiwxLjYxLDEuMTUsMS42MywxLjY2aDEuNzljLTAuMDgtMS45OC0xLjQ5LTMuMTktMy40NS0zLjE5QzkuNjQsNy42MSw4LDksOCwxMi4xNCBjMCwxLjk0LDAuOTMsNC4yNCwzLjg0LDQuMjRjMi4yMiwwLDMuNDEtMS42NSwzLjQ0LTIuOTVoLTEuNzljLTAuMDMsMC41OS0wLjQ1LDEuMzgtMS42MywxLjQ0QzEwLjU1LDE0LjgzLDEwLDEzLjgxLDEwLDEyLjE0IEMxMCw5LjI1LDExLjI4LDkuMTYsMTEuODgsOS4xNHogTTEyLDJDNi40OCwyLDIsNi40OCwyLDEyczQuNDgsMTAsMTAsMTBzMTAtNC40OCwxMC0xMFMxNy41MiwyLDEyLDJ6IE0xMiwyMGMtNC40MSwwLTgtMy41OS04LTggczMuNTktOCw4LThzOCwzLjU5LDgsOFMxNi40MSwyMCwxMiwyMHoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-cut: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTkuNjQgNy42NGMuMjMtLjUuMzYtMS4wNS4zNi0xLjY0IDAtMi4yMS0xLjc5LTQtNC00UzIgMy43OSAyIDZzMS43OSA0IDQgNGMuNTkgMCAxLjE0LS4xMyAxLjY0LS4zNkwxMCAxMmwtMi4zNiAyLjM2QzcuMTQgMTQuMTMgNi41OSAxNCA2IDE0Yy0yLjIxIDAtNCAxLjc5LTQgNHMxLjc5IDQgNCA0IDQtMS43OSA0LTRjMC0uNTktLjEzLTEuMTQtLjM2LTEuNjRMMTIgMTRsNyA3aDN2LTFMOS42NCA3LjY0ek02IDhjLTEuMSAwLTItLjg5LTItMnMuOS0yIDItMiAyIC44OSAyIDItLjkgMi0yIDJ6bTAgMTJjLTEuMSAwLTItLjg5LTItMnMuOS0yIDItMiAyIC44OSAyIDItLjkgMi0yIDJ6bTYtNy41Yy0uMjggMC0uNS0uMjItLjUtLjVzLjIyLS41LjUtLjUuNS4yMi41LjUtLjIyLjUtLjUuNXpNMTkgM2wtNiA2IDIgMiA3LTdWM3oiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-delete: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCIgd2lkdGg9IjE2cHgiIGhlaWdodD0iMTZweCI+CiAgICA8cGF0aCBkPSJNMCAwaDI0djI0SDB6IiBmaWxsPSJub25lIiAvPgogICAgPHBhdGggY2xhc3M9ImpwLWljb24zIiBmaWxsPSIjNjI2MjYyIiBkPSJNNiAxOWMwIDEuMS45IDIgMiAyaDhjMS4xIDAgMi0uOSAyLTJWN0g2djEyek0xOSA0aC0zLjVsLTEtMWgtNWwtMSAxSDV2MmgxNFY0eiIgLz4KPC9zdmc+Cg==);
  --jp-icon-download: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTE5IDloLTRWM0g5djZINWw3IDcgNy03ek01IDE4djJoMTR2LTJINXoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-duplicate: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTQiIGhlaWdodD0iMTQiIHZpZXdCb3g9IjAgMCAxNCAxNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPHBhdGggY2xhc3M9ImpwLWljb24zIiBmaWxsLXJ1bGU9ImV2ZW5vZGQiIGNsaXAtcnVsZT0iZXZlbm9kZCIgZD0iTTIuNzk5OTggMC44NzVIOC44OTU4MkM5LjIwMDYxIDAuODc1IDkuNDQ5OTggMS4xMzkxNCA5LjQ0OTk4IDEuNDYxOThDOS40NDk5OCAxLjc4NDgyIDkuMjAwNjEgMi4wNDg5NiA4Ljg5NTgyIDIuMDQ4OTZIMy4zNTQxNUMzLjA0OTM2IDIuMDQ4OTYgMi43OTk5OCAyLjMxMzEgMi43OTk5OCAyLjYzNTk0VjkuNjc5NjlDMi43OTk5OCAxMC4wMDI1IDIuNTUwNjEgMTAuMjY2NyAyLjI0NTgyIDEwLjI2NjdDMS45NDEwMyAxMC4yNjY3IDEuNjkxNjUgMTAuMDAyNSAxLjY5MTY1IDkuNjc5NjlWMi4wNDg5NkMxLjY5MTY1IDEuNDAzMjggMi4xOTA0IDAuODc1IDIuNzk5OTggMC44NzVaTTUuMzY2NjUgMTEuOVY0LjU1SDExLjA4MzNWMTEuOUg1LjM2NjY1Wk00LjE0MTY1IDQuMTQxNjdDNC4xNDE2NSAzLjY5MDYzIDQuNTA3MjggMy4zMjUgNC45NTgzMiAzLjMyNUgxMS40OTE3QzExLjk0MjcgMy4zMjUgMTIuMzA4MyAzLjY5MDYzIDEyLjMwODMgNC4xNDE2N1YxMi4zMDgzQzEyLjMwODMgMTIuNzU5NCAxMS45NDI3IDEzLjEyNSAxMS40OTE3IDEzLjEyNUg0Ljk1ODMyQzQuNTA3MjggMTMuMTI1IDQuMTQxNjUgMTIuNzU5NCA0LjE0MTY1IDEyLjMwODNWNC4xNDE2N1oiIGZpbGw9IiM2MTYxNjEiLz4KPHBhdGggY2xhc3M9ImpwLWljb24zIiBkPSJNOS40MzU3NCA4LjI2NTA3SDguMzY0MzFWOS4zMzY1QzguMzY0MzEgOS40NTQzNSA4LjI2Nzg4IDkuNTUwNzggOC4xNTAwMiA5LjU1MDc4QzguMDMyMTcgOS41NTA3OCA3LjkzNTc0IDkuNDU0MzUgNy45MzU3NCA5LjMzNjVWOC4yNjUwN0g2Ljg2NDMxQzYuNzQ2NDUgOC4yNjUwNyA2LjY1MDAyIDguMTY4NjQgNi42NTAwMiA4LjA1MDc4QzYuNjUwMDIgNy45MzI5MiA2Ljc0NjQ1IDcuODM2NSA2Ljg2NDMxIDcuODM2NUg3LjkzNTc0VjYuNzY1MDdDNy45MzU3NCA2LjY0NzIxIDguMDMyMTcgNi41NTA3OCA4LjE1MDAyIDYuNTUwNzhDOC4yNjc4OCA2LjU1MDc4IDguMzY0MzEgNi42NDcyMSA4LjM2NDMxIDYuNzY1MDdWNy44MzY1SDkuNDM1NzRDOS41NTM2IDcuODM2NSA5LjY1MDAyIDcuOTMyOTIgOS42NTAwMiA4LjA1MDc4QzkuNjUwMDIgOC4xNjg2NCA5LjU1MzYgOC4yNjUwNyA5LjQzNTc0IDguMjY1MDdaIiBmaWxsPSIjNjE2MTYxIiBzdHJva2U9IiM2MTYxNjEiIHN0cm9rZS13aWR0aD0iMC41Ii8+Cjwvc3ZnPgo=);
  --jp-icon-edit: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTMgMTcuMjVWMjFoMy43NUwxNy44MSA5Ljk0bC0zLjc1LTMuNzVMMyAxNy4yNXpNMjAuNzEgNy4wNGMuMzktLjM5LjM5LTEuMDIgMC0xLjQxbC0yLjM0LTIuMzRjLS4zOS0uMzktMS4wMi0uMzktMS40MSAwbC0xLjgzIDEuODMgMy43NSAzLjc1IDEuODMtMS44M3oiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-ellipses: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPGNpcmNsZSBjeD0iNSIgY3k9IjEyIiByPSIyIi8+CiAgICA8Y2lyY2xlIGN4PSIxMiIgY3k9IjEyIiByPSIyIi8+CiAgICA8Y2lyY2xlIGN4PSIxOSIgY3k9IjEyIiByPSIyIi8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-error: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KPGcgY2xhc3M9ImpwLWljb24zIiBmaWxsPSIjNjE2MTYxIj48Y2lyY2xlIGN4PSIxMiIgY3k9IjE5IiByPSIyIi8+PHBhdGggZD0iTTEwIDNoNHYxMmgtNHoiLz48L2c+CjxwYXRoIGZpbGw9Im5vbmUiIGQ9Ik0wIDBoMjR2MjRIMHoiLz4KPC9zdmc+Cg==);
  --jp-icon-expand-all: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGgKICAgICAgICAgICAgZD0iTTggMmMxIDAgMTEgMCAxMiAwczIgMSAyIDJjMCAxIDAgMTEgMCAxMnMwIDItMiAyQzIwIDE0IDIwIDQgMjAgNFMxMCA0IDYgNGMwLTIgMS0yIDItMnoiIC8+CiAgICAgICAgPHBhdGgKICAgICAgICAgICAgZD0iTTE4IDhjMC0xLTEtMi0yLTJTNSA2IDQgNnMtMiAxLTIgMmMwIDEgMCAxMSAwIDEyczEgMiAyIDJjMSAwIDExIDAgMTIgMHMyLTEgMi0yYzAtMSAwLTExIDAtMTJ6bS0yIDB2MTJINFY4eiIgLz4KICAgICAgICA8cGF0aCBkPSJNMTEgMTBIOXYzSDZ2MmgzdjNoMnYtM2gzdi0yaC0zeiIgLz4KICAgIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-extension: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTIwLjUgMTFIMTlWN2MwLTEuMS0uOS0yLTItMmgtNFYzLjVDMTMgMi4xMiAxMS44OCAxIDEwLjUgMVM4IDIuMTIgOCAzLjVWNUg0Yy0xLjEgMC0xLjk5LjktMS45OSAydjMuOEgzLjVjMS40OSAwIDIuNyAxLjIxIDIuNyAyLjdzLTEuMjEgMi43LTIuNyAyLjdIMlYyMGMwIDEuMS45IDIgMiAyaDMuOHYtMS41YzAtMS40OSAxLjIxLTIuNyAyLjctMi43IDEuNDkgMCAyLjcgMS4yMSAyLjcgMi43VjIySDE3YzEuMSAwIDItLjkgMi0ydi00aDEuNWMxLjM4IDAgMi41LTEuMTIgMi41LTIuNVMyMS44OCAxMSAyMC41IDExeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-fast-forward: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyNCIgaGVpZ2h0PSIyNCIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTQgMThsOC41LTZMNCA2djEyem05LTEydjEybDguNS02TDEzIDZ6Ii8+CiAgICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-file-upload: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTkgMTZoNnYtNmg0bC03LTctNyA3aDR6bS00IDJoMTR2Mkg1eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-file: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMTkuMyA4LjJsLTUuNS01LjVjLS4zLS4zLS43LS41LTEuMi0uNUgzLjljLS44LjEtMS42LjktMS42IDEuOHYxNC4xYzAgLjkuNyAxLjYgMS42IDEuNmgxNC4yYy45IDAgMS42LS43IDEuNi0xLjZWOS40Yy4xLS41LS4xLS45LS40LTEuMnptLTUuOC0zLjNsMy40IDMuNmgtMy40VjQuOXptMy45IDEyLjdINC43Yy0uMSAwLS4yIDAtLjItLjJWNC43YzAtLjIuMS0uMy4yLS4zaDcuMnY0LjRzMCAuOC4zIDEuMWMuMy4zIDEuMS4zIDEuMS4zaDQuM3Y3LjJzLS4xLjItLjIuMnoiLz4KPC9zdmc+Cg==);
  --jp-icon-filter-dot: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiNGRkYiPgogICAgPHBhdGggZD0iTTE0LDEyVjE5Ljg4QzE0LjA0LDIwLjE4IDEzLjk0LDIwLjUgMTMuNzEsMjAuNzFDMTMuMzIsMjEuMSAxMi42OSwyMS4xIDEyLjMsMjAuNzFMMTAuMjksMTguN0MxMC4wNiwxOC40NyA5Ljk2LDE4LjE2IDEwLDE3Ljg3VjEySDkuOTdMNC4yMSw0LjYyQzMuODcsNC4xOSAzLjk1LDMuNTYgNC4zOCwzLjIyQzQuNTcsMy4wOCA0Ljc4LDMgNSwzVjNIMTlWM0MxOS4yMiwzIDE5LjQzLDMuMDggMTkuNjIsMy4yMkMyMC4wNSwzLjU2IDIwLjEzLDQuMTkgMTkuNzksNC42MkwxNC4wMywxMkgxNFoiIC8+CiAgPC9nPgogIDxnIGNsYXNzPSJqcC1pY29uLWRvdCIgZmlsbD0iI0ZGRiI+CiAgICA8Y2lyY2xlIGN4PSIxOCIgY3k9IjE3IiByPSIzIj48L2NpcmNsZT4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-filter-list: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEwIDE4aDR2LTJoLTR2MnpNMyA2djJoMThWNkgzem0zIDdoMTJ2LTJINnYyeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-filter: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiNGRkYiPgogICAgPHBhdGggZD0iTTE0LDEyVjE5Ljg4QzE0LjA0LDIwLjE4IDEzLjk0LDIwLjUgMTMuNzEsMjAuNzFDMTMuMzIsMjEuMSAxMi42OSwyMS4xIDEyLjMsMjAuNzFMMTAuMjksMTguN0MxMC4wNiwxOC40NyA5Ljk2LDE4LjE2IDEwLDE3Ljg3VjEySDkuOTdMNC4yMSw0LjYyQzMuODcsNC4xOSAzLjk1LDMuNTYgNC4zOCwzLjIyQzQuNTcsMy4wOCA0Ljc4LDMgNSwzVjNIMTlWM0MxOS4yMiwzIDE5LjQzLDMuMDggMTkuNjIsMy4yMkMyMC4wNSwzLjU2IDIwLjEzLDQuMTkgMTkuNzksNC42MkwxNC4wMywxMkgxNFoiIC8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-folder-favorite: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIGhlaWdodD0iMjRweCIgdmlld0JveD0iMCAwIDI0IDI0IiB3aWR0aD0iMjRweCIgZmlsbD0iIzAwMDAwMCI+CiAgPHBhdGggZD0iTTAgMGgyNHYyNEgwVjB6IiBmaWxsPSJub25lIi8+PHBhdGggY2xhc3M9ImpwLWljb24zIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iIzYxNjE2MSIgZD0iTTIwIDZoLThsLTItMkg0Yy0xLjEgMC0yIC45LTIgMnYxMmMwIDEuMS45IDIgMiAyaDE2YzEuMSAwIDItLjkgMi0yVjhjMC0xLjEtLjktMi0yLTJ6bS0yLjA2IDExTDE1IDE1LjI4IDEyLjA2IDE3bC43OC0zLjMzLTIuNTktMi4yNCAzLjQxLS4yOUwxNSA4bDEuMzQgMy4xNCAzLjQxLjI5LTIuNTkgMi4yNC43OCAzLjMzeiIvPgo8L3N2Zz4K);
  --jp-icon-folder: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMTAgNEg0Yy0xLjEgMC0xLjk5LjktMS45OSAyTDIgMThjMCAxLjEuOSAyIDIgMmgxNmMxLjEgMCAyLS45IDItMlY4YzAtMS4xLS45LTItMi0yaC04bC0yLTJ6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-home: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIGhlaWdodD0iMjRweCIgdmlld0JveD0iMCAwIDI0IDI0IiB3aWR0aD0iMjRweCIgZmlsbD0iIzAwMDAwMCI+CiAgPHBhdGggZD0iTTAgMGgyNHYyNEgweiIgZmlsbD0ibm9uZSIvPjxwYXRoIGNsYXNzPSJqcC1pY29uMyBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiM2MTYxNjEiIGQ9Ik0xMCAyMHYtNmg0djZoNXYtOGgzTDEyIDMgMiAxMmgzdjh6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-html5: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDUxMiA1MTIiPgogIDxwYXRoIGNsYXNzPSJqcC1pY29uMCBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiMwMDAiIGQ9Ik0xMDguNCAwaDIzdjIyLjhoMjEuMlYwaDIzdjY5aC0yM1Y0NmgtMjF2MjNoLTIzLjJNMjA2IDIzaC0yMC4zVjBoNjMuN3YyM0gyMjl2NDZoLTIzbTUzLjUtNjloMjQuMWwxNC44IDI0LjNMMzEzLjIgMGgyNC4xdjY5aC0yM1YzNC44bC0xNi4xIDI0LjgtMTYuMS0yNC44VjY5aC0yMi42bTg5LjItNjloMjN2NDYuMmgzMi42VjY5aC01NS42Ii8+CiAgPHBhdGggY2xhc3M9ImpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iI2U0NGQyNiIgZD0iTTEwNy42IDQ3MWwtMzMtMzcwLjRoMzYyLjhsLTMzIDM3MC4yTDI1NS43IDUxMiIvPgogIDxwYXRoIGNsYXNzPSJqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiNmMTY1MjkiIGQ9Ik0yNTYgNDgwLjVWMTMxaDE0OC4zTDM3NiA0NDciLz4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1zZWxlY3RhYmxlLWludmVyc2UiIGZpbGw9IiNlYmViZWIiIGQ9Ik0xNDIgMTc2LjNoMTE0djQ1LjRoLTY0LjJsNC4yIDQ2LjVoNjB2NDUuM0gxNTQuNG0yIDIyLjhIMjAybDMuMiAzNi4zIDUwLjggMTMuNnY0Ny40bC05My4yLTI2Ii8+CiAgPHBhdGggY2xhc3M9ImpwLWljb24tc2VsZWN0YWJsZS1pbnZlcnNlIiBmaWxsPSIjZmZmIiBkPSJNMzY5LjYgMTc2LjNIMjU1Ljh2NDUuNGgxMDkuNm0tNC4xIDQ2LjVIMjU1Ljh2NDUuNGg1NmwtNS4zIDU5LTUwLjcgMTMuNnY0Ny4ybDkzLTI1LjgiLz4KPC9zdmc+Cg==);
  --jp-icon-image: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1icmFuZDQganAtaWNvbi1zZWxlY3RhYmxlLWludmVyc2UiIGZpbGw9IiNGRkYiIGQ9Ik0yLjIgMi4yaDE3LjV2MTcuNUgyLjJ6Ii8+CiAgPHBhdGggY2xhc3M9ImpwLWljb24tYnJhbmQwIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iIzNGNTFCNSIgZD0iTTIuMiAyLjJ2MTcuNWgxNy41bC4xLTE3LjVIMi4yem0xMi4xIDIuMmMxLjIgMCAyLjIgMSAyLjIgMi4ycy0xIDIuMi0yLjIgMi4yLTIuMi0xLTIuMi0yLjIgMS0yLjIgMi4yLTIuMnpNNC40IDE3LjZsMy4zLTguOCAzLjMgNi42IDIuMi0zLjIgNC40IDUuNEg0LjR6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-info: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDUwLjk3OCA1MC45NzgiPgoJPGcgY2xhc3M9ImpwLWljb24zIiBmaWxsPSIjNjE2MTYxIj4KCQk8cGF0aCBkPSJNNDMuNTIsNy40NThDMzguNzExLDIuNjQ4LDMyLjMwNywwLDI1LjQ4OSwwQzE4LjY3LDAsMTIuMjY2LDIuNjQ4LDcuNDU4LDcuNDU4CgkJCWMtOS45NDMsOS45NDEtOS45NDMsMjYuMTE5LDAsMzYuMDYyYzQuODA5LDQuODA5LDExLjIxMiw3LjQ1NiwxOC4wMzEsNy40NThjMCwwLDAuMDAxLDAsMC4wMDIsMAoJCQljNi44MTYsMCwxMy4yMjEtMi42NDgsMTguMDI5LTcuNDU4YzQuODA5LTQuODA5LDcuNDU3LTExLjIxMiw3LjQ1Ny0xOC4wM0M1MC45NzcsMTguNjcsNDguMzI4LDEyLjI2Niw0My41Miw3LjQ1OHoKCQkJIE00Mi4xMDYsNDIuMTA1Yy00LjQzMiw0LjQzMS0xMC4zMzIsNi44NzItMTYuNjE1LDYuODcyaC0wLjAwMmMtNi4yODUtMC4wMDEtMTIuMTg3LTIuNDQxLTE2LjYxNy02Ljg3MgoJCQljLTkuMTYyLTkuMTYzLTkuMTYyLTI0LjA3MSwwLTMzLjIzM0MxMy4zMDMsNC40NCwxOS4yMDQsMiwyNS40ODksMmM2LjI4NCwwLDEyLjE4NiwyLjQ0LDE2LjYxNyw2Ljg3MgoJCQljNC40MzEsNC40MzEsNi44NzEsMTAuMzMyLDYuODcxLDE2LjYxN0M0OC45NzcsMzEuNzcyLDQ2LjUzNiwzNy42NzUsNDIuMTA2LDQyLjEwNXoiLz4KCQk8cGF0aCBkPSJNMjMuNTc4LDMyLjIxOGMtMC4wMjMtMS43MzQsMC4xNDMtMy4wNTksMC40OTYtMy45NzJjMC4zNTMtMC45MTMsMS4xMS0xLjk5NywyLjI3Mi0zLjI1MwoJCQljMC40NjgtMC41MzYsMC45MjMtMS4wNjIsMS4zNjctMS41NzVjMC42MjYtMC43NTMsMS4xMDQtMS40NzgsMS40MzYtMi4xNzVjMC4zMzEtMC43MDcsMC40OTUtMS41NDEsMC40OTUtMi41CgkJCWMwLTEuMDk2LTAuMjYtMi4wODgtMC43NzktMi45NzljLTAuNTY1LTAuODc5LTEuNTAxLTEuMzM2LTIuODA2LTEuMzY5Yy0xLjgwMiwwLjA1Ny0yLjk4NSwwLjY2Ny0zLjU1LDEuODMyCgkJCWMtMC4zMDEsMC41MzUtMC41MDMsMS4xNDEtMC42MDcsMS44MTRjLTAuMTM5LDAuNzA3LTAuMjA3LDEuNDMyLTAuMjA3LDIuMTc0aC0yLjkzN2MtMC4wOTEtMi4yMDgsMC40MDctNC4xMTQsMS40OTMtNS43MTkKCQkJYzEuMDYyLTEuNjQsMi44NTUtMi40ODEsNS4zNzgtMi41MjdjMi4xNiwwLjAyMywzLjg3NCwwLjYwOCw1LjE0MSwxLjc1OGMxLjI3OCwxLjE2LDEuOTI5LDIuNzY0LDEuOTUsNC44MTEKCQkJYzAsMS4xNDItMC4xMzcsMi4xMTEtMC40MSwyLjkxMWMtMC4zMDksMC44NDUtMC43MzEsMS41OTMtMS4yNjgsMi4yNDNjLTAuNDkyLDAuNjUtMS4wNjgsMS4zMTgtMS43MywyLjAwMgoJCQljLTAuNjUsMC42OTctMS4zMTMsMS40NzktMS45ODcsMi4zNDZjLTAuMjM5LDAuMzc3LTAuNDI5LDAuNzc3LTAuNTY1LDEuMTk5Yy0wLjE2LDAuOTU5LTAuMjE3LDEuOTUxLTAuMTcxLDIuOTc5CgkJCUMyNi41ODksMzIuMjE4LDIzLjU3OCwzMi4yMTgsMjMuNTc4LDMyLjIxOHogTTIzLjU3OCwzOC4yMnYtMy40ODRoMy4wNzZ2My40ODRIMjMuNTc4eiIvPgoJPC9nPgo8L3N2Zz4K);
  --jp-icon-inspector: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaW5zcGVjdG9yLWljb24tY29sb3IganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMjAgNEg0Yy0xLjEgMC0xLjk5LjktMS45OSAyTDIgMThjMCAxLjEuOSAyIDIgMmgxNmMxLjEgMCAyLS45IDItMlY2YzAtMS4xLS45LTItMi0yem0tNSAxNEg0di00aDExdjR6bTAtNUg0VjloMTF2NHptNSA1aC00VjloNHY5eiIvPgo8L3N2Zz4K);
  --jp-icon-json: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8ZyBjbGFzcz0ianAtanNvbi1pY29uLWNvbG9yIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iI0Y5QTgyNSI+CiAgICA8cGF0aCBkPSJNMjAuMiAxMS44Yy0xLjYgMC0xLjcuNS0xLjcgMSAwIC40LjEuOS4xIDEuMy4xLjUuMS45LjEgMS4zIDAgMS43LTEuNCAyLjMtMy41IDIuM2gtLjl2LTEuOWguNWMxLjEgMCAxLjQgMCAxLjQtLjggMC0uMyAwLS42LS4xLTEgMC0uNC0uMS0uOC0uMS0xLjIgMC0xLjMgMC0xLjggMS4zLTItMS4zLS4yLTEuMy0uNy0xLjMtMiAwLS40LjEtLjguMS0xLjIuMS0uNC4xLS43LjEtMSAwLS44LS40LS43LTEuNC0uOGgtLjVWNC4xaC45YzIuMiAwIDMuNS43IDMuNSAyLjMgMCAuNC0uMS45LS4xIDEuMy0uMS41LS4xLjktLjEgMS4zIDAgLjUuMiAxIDEuNyAxdjEuOHpNMS44IDEwLjFjMS42IDAgMS43LS41IDEuNy0xIDAtLjQtLjEtLjktLjEtMS4zLS4xLS41LS4xLS45LS4xLTEuMyAwLTEuNiAxLjQtMi4zIDMuNS0yLjNoLjl2MS45aC0uNWMtMSAwLTEuNCAwLTEuNC44IDAgLjMgMCAuNi4xIDEgMCAuMi4xLjYuMSAxIDAgMS4zIDAgMS44LTEuMyAyQzYgMTEuMiA2IDExLjcgNiAxM2MwIC40LS4xLjgtLjEgMS4yLS4xLjMtLjEuNy0uMSAxIDAgLjguMy44IDEuNC44aC41djEuOWgtLjljLTIuMSAwLTMuNS0uNi0zLjUtMi4zIDAtLjQuMS0uOS4xLTEuMy4xLS41LjEtLjkuMS0xLjMgMC0uNS0uMi0xLTEuNy0xdi0xLjl6Ii8+CiAgICA8Y2lyY2xlIGN4PSIxMSIgY3k9IjEzLjgiIHI9IjIuMSIvPgogICAgPGNpcmNsZSBjeD0iMTEiIGN5PSI4LjIiIHI9IjIuMSIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-julia: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDMyNSAzMDAiPgogIDxnIGNsYXNzPSJqcC1icmFuZDAganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjY2IzYzMzIj4KICAgIDxwYXRoIGQ9Ik0gMTUwLjg5ODQzOCAyMjUgQyAxNTAuODk4NDM4IDI2Ni40MjE4NzUgMTE3LjMyMDMxMiAzMDAgNzUuODk4NDM4IDMwMCBDIDM0LjQ3NjU2MiAzMDAgMC44OTg0MzggMjY2LjQyMTg3NSAwLjg5ODQzOCAyMjUgQyAwLjg5ODQzOCAxODMuNTc4MTI1IDM0LjQ3NjU2MiAxNTAgNzUuODk4NDM4IDE1MCBDIDExNy4zMjAzMTIgMTUwIDE1MC44OTg0MzggMTgzLjU3ODEyNSAxNTAuODk4NDM4IDIyNSIvPgogIDwvZz4KICA8ZyBjbGFzcz0ianAtYnJhbmQwIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iIzM4OTgyNiI+CiAgICA8cGF0aCBkPSJNIDIzNy41IDc1IEMgMjM3LjUgMTE2LjQyMTg3NSAyMDMuOTIxODc1IDE1MCAxNjIuNSAxNTAgQyAxMjEuMDc4MTI1IDE1MCA4Ny41IDExNi40MjE4NzUgODcuNSA3NSBDIDg3LjUgMzMuNTc4MTI1IDEyMS4wNzgxMjUgMCAxNjIuNSAwIEMgMjAzLjkyMTg3NSAwIDIzNy41IDMzLjU3ODEyNSAyMzcuNSA3NSIvPgogIDwvZz4KICA8ZyBjbGFzcz0ianAtYnJhbmQwIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iIzk1NThiMiI+CiAgICA8cGF0aCBkPSJNIDMyNC4xMDE1NjIgMjI1IEMgMzI0LjEwMTU2MiAyNjYuNDIxODc1IDI5MC41MjM0MzggMzAwIDI0OS4xMDE1NjIgMzAwIEMgMjA3LjY3OTY4OCAzMDAgMTc0LjEwMTU2MiAyNjYuNDIxODc1IDE3NC4xMDE1NjIgMjI1IEMgMTc0LjEwMTU2MiAxODMuNTc4MTI1IDIwNy42Nzk2ODggMTUwIDI0OS4xMDE1NjIgMTUwIEMgMjkwLjUyMzQzOCAxNTAgMzI0LjEwMTU2MiAxODMuNTc4MTI1IDMyNC4xMDE1NjIgMjI1Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-jupyter-favicon: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTUyIiBoZWlnaHQ9IjE2NSIgdmlld0JveD0iMCAwIDE1MiAxNjUiIHZlcnNpb249IjEuMSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgPGcgY2xhc3M9ImpwLWp1cHl0ZXItaWNvbi1jb2xvciIgZmlsbD0iI0YzNzcyNiI+CiAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgwLjA3ODk0NywgMTEwLjU4MjkyNykiIGQ9Ik03NS45NDIyODQyLDI5LjU4MDQ1NjEgQzQzLjMwMjM5NDcsMjkuNTgwNDU2MSAxNC43OTY3ODMyLDE3LjY1MzQ2MzQgMCwwIEM1LjUxMDgzMjExLDE1Ljg0MDY4MjkgMTUuNzgxNTM4OSwyOS41NjY3NzMyIDI5LjM5MDQ5NDcsMzkuMjc4NDE3MSBDNDIuOTk5Nyw0OC45ODk4NTM3IDU5LjI3MzcsNTQuMjA2NzgwNSA3NS45NjA1Nzg5LDU0LjIwNjc4MDUgQzkyLjY0NzQ1NzksNTQuMjA2NzgwNSAxMDguOTIxNDU4LDQ4Ljk4OTg1MzcgMTIyLjUzMDY2MywzOS4yNzg0MTcxIEMxMzYuMTM5NDUzLDI5LjU2Njc3MzIgMTQ2LjQxMDI4NCwxNS44NDA2ODI5IDE1MS45MjExNTgsMCBDMTM3LjA4Nzg2OCwxNy42NTM0NjM0IDEwOC41ODI1ODksMjkuNTgwNDU2MSA3NS45NDIyODQyLDI5LjU4MDQ1NjEgTDc1Ljk0MjI4NDIsMjkuNTgwNDU2MSBaIiAvPgogICAgPHBhdGggdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMC4wMzczNjgsIDAuNzA0ODc4KSIgZD0iTTc1Ljk3ODQ1NzksMjQuNjI2NDA3MyBDMTA4LjYxODc2MywyNC42MjY0MDczIDEzNy4xMjQ0NTgsMzYuNTUzNDQxNSAxNTEuOTIxMTU4LDU0LjIwNjc4MDUgQzE0Ni40MTAyODQsMzguMzY2MjIyIDEzNi4xMzk0NTMsMjQuNjQwMTMxNyAxMjIuNTMwNjYzLDE0LjkyODQ4NzggQzEwOC45MjE0NTgsNS4yMTY4NDM5IDkyLjY0NzQ1NzksMCA3NS45NjA1Nzg5LDAgQzU5LjI3MzcsMCA0Mi45OTk3LDUuMjE2ODQzOSAyOS4zOTA0OTQ3LDE0LjkyODQ4NzggQzE1Ljc4MTUzODksMjQuNjQwMTMxNyA1LjUxMDgzMjExLDM4LjM2NjIyMiAwLDU0LjIwNjc4MDUgQzE0LjgzMzA4MTYsMzYuNTg5OTI5MyA0My4zMzg1Njg0LDI0LjYyNjQwNzMgNzUuOTc4NDU3OSwyNC42MjY0MDczIEw3NS45Nzg0NTc5LDI0LjYyNjQwNzMgWiIgLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-jupyter: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMzkiIGhlaWdodD0iNTEiIHZpZXdCb3g9IjAgMCAzOSA1MSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMTYzOCAtMjI4MSkiPgogICAgIDxnIGNsYXNzPSJqcC1qdXB5dGVyLWljb24tY29sb3IiIGZpbGw9IiNGMzc3MjYiPgogICAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxNjM5Ljc0IDIzMTEuOTgpIiBkPSJNIDE4LjI2NDYgNy4xMzQxMUMgMTAuNDE0NSA3LjEzNDExIDMuNTU4NzIgNC4yNTc2IDAgMEMgMS4zMjUzOSAzLjgyMDQgMy43OTU1NiA3LjEzMDgxIDcuMDY4NiA5LjQ3MzAzQyAxMC4zNDE3IDExLjgxNTIgMTQuMjU1NyAxMy4wNzM0IDE4LjI2OSAxMy4wNzM0QyAyMi4yODIzIDEzLjA3MzQgMjYuMTk2MyAxMS44MTUyIDI5LjQ2OTQgOS40NzMwM0MgMzIuNzQyNCA3LjEzMDgxIDM1LjIxMjYgMy44MjA0IDM2LjUzOCAwQyAzMi45NzA1IDQuMjU3NiAyNi4xMTQ4IDcuMTM0MTEgMTguMjY0NiA3LjEzNDExWiIvPgogICAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxNjM5LjczIDIyODUuNDgpIiBkPSJNIDE4LjI3MzMgNS45MzkzMUMgMjYuMTIzNSA1LjkzOTMxIDMyLjk3OTMgOC44MTU4MyAzNi41MzggMTMuMDczNEMgMzUuMjEyNiA5LjI1MzAzIDMyLjc0MjQgNS45NDI2MiAyOS40Njk0IDMuNjAwNEMgMjYuMTk2MyAxLjI1ODE4IDIyLjI4MjMgMCAxOC4yNjkgMEMgMTQuMjU1NyAwIDEwLjM0MTcgMS4yNTgxOCA3LjA2ODYgMy42MDA0QyAzLjc5NTU2IDUuOTQyNjIgMS4zMjUzOSA5LjI1MzAzIDAgMTMuMDczNEMgMy41Njc0NSA4LjgyNDYzIDEwLjQyMzIgNS45MzkzMSAxOC4yNzMzIDUuOTM5MzFaIi8+CiAgICA8L2c+CiAgICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxNjY5LjMgMjI4MS4zMSkiIGQ9Ik0gNS44OTM1MyAyLjg0NEMgNS45MTg4OSAzLjQzMTY1IDUuNzcwODUgNC4wMTM2NyA1LjQ2ODE1IDQuNTE2NDVDIDUuMTY1NDUgNS4wMTkyMiA0LjcyMTY4IDUuNDIwMTUgNC4xOTI5OSA1LjY2ODUxQyAzLjY2NDMgNS45MTY4OCAzLjA3NDQ0IDYuMDAxNTEgMi40OTgwNSA1LjkxMTcxQyAxLjkyMTY2IDUuODIxOSAxLjM4NDYzIDUuNTYxNyAwLjk1NDg5OCA1LjE2NDAxQyAwLjUyNTE3IDQuNzY2MzMgMC4yMjIwNTYgNC4yNDkwMyAwLjA4MzkwMzcgMy42Nzc1N0MgLTAuMDU0MjQ4MyAzLjEwNjExIC0wLjAyMTIzIDIuNTA2MTcgMC4xNzg3ODEgMS45NTM2NEMgMC4zNzg3OTMgMS40MDExIDAuNzM2ODA5IDAuOTIwODE3IDEuMjA3NTQgMC41NzM1MzhDIDEuNjc4MjYgMC4yMjYyNTkgMi4yNDA1NSAwLjAyNzU5MTkgMi44MjMyNiAwLjAwMjY3MjI5QyAzLjYwMzg5IC0wLjAzMDcxMTUgNC4zNjU3MyAwLjI0OTc4OSA0Ljk0MTQyIDAuNzgyNTUxQyA1LjUxNzExIDEuMzE1MzEgNS44NTk1NiAyLjA1Njc2IDUuODkzNTMgMi44NDRaIi8+CiAgICAgIDxwYXRoIHRyYW5zZm9ybT0idHJhbnNsYXRlKDE2MzkuOCAyMzIzLjgxKSIgZD0iTSA3LjQyNzg5IDMuNTgzMzhDIDcuNDYwMDggNC4zMjQzIDcuMjczNTUgNS4wNTgxOSA2Ljg5MTkzIDUuNjkyMTNDIDYuNTEwMzEgNi4zMjYwNyA1Ljk1MDc1IDYuODMxNTYgNS4yODQxMSA3LjE0NDZDIDQuNjE3NDcgNy40NTc2MyAzLjg3MzcxIDcuNTY0MTQgMy4xNDcwMiA3LjQ1MDYzQyAyLjQyMDMyIDcuMzM3MTIgMS43NDMzNiA3LjAwODcgMS4yMDE4NCA2LjUwNjk1QyAwLjY2MDMyOCA2LjAwNTIgMC4yNzg2MSA1LjM1MjY4IDAuMTA1MDE3IDQuNjMyMDJDIC0wLjA2ODU3NTcgMy45MTEzNSAtMC4wMjYyMzYxIDMuMTU0OTQgMC4yMjY2NzUgMi40NTg1NkMgMC40Nzk1ODcgMS43NjIxNyAwLjkzMTY5NyAxLjE1NzEzIDEuNTI1NzYgMC43MjAwMzNDIDIuMTE5ODMgMC4yODI5MzUgMi44MjkxNCAwLjAzMzQzOTUgMy41NjM4OSAwLjAwMzEzMzQ0QyA0LjU0NjY3IC0wLjAzNzQwMzMgNS41MDUyOSAwLjMxNjcwNiA2LjIyOTYxIDAuOTg3ODM1QyA2Ljk1MzkzIDEuNjU4OTYgNy4zODQ4NCAyLjU5MjM1IDcuNDI3ODkgMy41ODMzOEwgNy40Mjc4OSAzLjU4MzM4WiIvPgogICAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxNjM4LjM2IDIyODYuMDYpIiBkPSJNIDIuMjc0NzEgNC4zOTYyOUMgMS44NDM2MyA0LjQxNTA4IDEuNDE2NzEgNC4zMDQ0NSAxLjA0Nzk5IDQuMDc4NDNDIDAuNjc5MjY4IDMuODUyNCAwLjM4NTMyOCAzLjUyMTE0IDAuMjAzMzcxIDMuMTI2NTZDIDAuMDIxNDEzNiAyLjczMTk4IC0wLjA0MDM3OTggMi4yOTE4MyAwLjAyNTgxMTYgMS44NjE4MUMgMC4wOTIwMDMxIDEuNDMxOCAwLjI4MzIwNCAxLjAzMTI2IDAuNTc1MjEzIDAuNzEwODgzQyAwLjg2NzIyMiAwLjM5MDUxIDEuMjQ2OTEgMC4xNjQ3MDggMS42NjYyMiAwLjA2MjA1OTJDIDIuMDg1NTMgLTAuMDQwNTg5NyAyLjUyNTYxIC0wLjAxNTQ3MTQgMi45MzA3NiAwLjEzNDIzNUMgMy4zMzU5MSAwLjI4Mzk0MSAzLjY4NzkyIDAuNTUxNTA1IDMuOTQyMjIgMC45MDMwNkMgNC4xOTY1MiAxLjI1NDYyIDQuMzQxNjkgMS42NzQzNiA0LjM1OTM1IDIuMTA5MTZDIDQuMzgyOTkgMi42OTEwNyA0LjE3Njc4IDMuMjU4NjkgMy43ODU5NyAzLjY4NzQ2QyAzLjM5NTE2IDQuMTE2MjQgMi44NTE2NiA0LjM3MTE2IDIuMjc0NzEgNC4zOTYyOUwgMi4yNzQ3MSA0LjM5NjI5WiIvPgogICAgPC9nPgogIDwvZz4+Cjwvc3ZnPgo=);
  --jp-icon-jupyterlab-wordmark: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyMDAiIHZpZXdCb3g9IjAgMCAxODYwLjggNDc1Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjIiIGZpbGw9IiM0RTRFNEUiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDQ4MC4xMzY0MDEsIDY0LjI3MTQ5MykiPgogICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMC4wMDAwMDAsIDU4Ljg3NTU2NikiPgogICAgICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgwLjA4NzYwMywgMC4xNDAyOTQpIj4KICAgICAgICA8cGF0aCBkPSJNLTQyNi45LDE2OS44YzAsNDguNy0zLjcsNjQuNy0xMy42LDc2LjRjLTEwLjgsMTAtMjUsMTUuNS0zOS43LDE1LjVsMy43LDI5IGMyMi44LDAuMyw0NC44LTcuOSw2MS45LTIzLjFjMTcuOC0xOC41LDI0LTQ0LjEsMjQtODMuM1YwSC00Mjd2MTcwLjFMLTQyNi45LDE2OS44TC00MjYuOSwxNjkuOHoiLz4KICAgICAgPC9nPgogICAgPC9nPgogICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMTU1LjA0NTI5NiwgNTYuODM3MTA0KSI+CiAgICAgIDxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKDEuNTYyNDUzLCAxLjc5OTg0MikiPgogICAgICAgIDxwYXRoIGQ9Ik0tMzEyLDE0OGMwLDIxLDAsMzkuNSwxLjcsNTUuNGgtMzEuOGwtMi4xLTMzLjNoLTAuOGMtNi43LDExLjYtMTYuNCwyMS4zLTI4LDI3LjkgYy0xMS42LDYuNi0yNC44LDEwLTM4LjIsOS44Yy0zMS40LDAtNjktMTcuNy02OS04OVYwaDM2LjR2MTEyLjdjMCwzOC43LDExLjYsNjQuNyw0NC42LDY0LjdjMTAuMy0wLjIsMjAuNC0zLjUsMjguOS05LjQgYzguNS01LjksMTUuMS0xNC4zLDE4LjktMjMuOWMyLjItNi4xLDMuMy0xMi41LDMuMy0xOC45VjAuMmgzNi40VjE0OEgtMzEyTC0zMTIsMTQ4eiIvPgogICAgICA8L2c+CiAgICA8L2c+CiAgICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgzOTAuMDEzMzIyLCA1My40Nzk2MzgpIj4KICAgICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMS43MDY0NTgsIDAuMjMxNDI1KSI+CiAgICAgICAgPHBhdGggZD0iTS00NzguNiw3MS40YzAtMjYtMC44LTQ3LTEuNy02Ni43aDMyLjdsMS43LDM0LjhoMC44YzcuMS0xMi41LDE3LjUtMjIuOCwzMC4xLTI5LjcgYzEyLjUtNywyNi43LTEwLjMsNDEtOS44YzQ4LjMsMCw4NC43LDQxLjcsODQuNywxMDMuM2MwLDczLjEtNDMuNywxMDkuMi05MSwxMDkuMmMtMTIuMSwwLjUtMjQuMi0yLjItMzUtNy44IGMtMTAuOC01LjYtMTkuOS0xMy45LTI2LjYtMjQuMmgtMC44VjI5MWgtMzZ2LTIyMEwtNDc4LjYsNzEuNEwtNDc4LjYsNzEuNHogTS00NDIuNiwxMjUuNmMwLjEsNS4xLDAuNiwxMC4xLDEuNywxNS4xIGMzLDEyLjMsOS45LDIzLjMsMTkuOCwzMS4xYzkuOSw3LjgsMjIuMSwxMi4xLDM0LjcsMTIuMWMzOC41LDAsNjAuNy0zMS45LDYwLjctNzguNWMwLTQwLjctMjEuMS03NS42LTU5LjUtNzUuNiBjLTEyLjksMC40LTI1LjMsNS4xLTM1LjMsMTMuNGMtOS45LDguMy0xNi45LDE5LjctMTkuNiwzMi40Yy0xLjUsNC45LTIuMywxMC0yLjUsMTUuMVYxMjUuNkwtNDQyLjYsMTI1LjZMLTQ0Mi42LDEyNS42eiIvPgogICAgICA8L2c+CiAgICA8L2c+CiAgICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSg2MDYuNzQwNzI2LCA1Ni44MzcxMDQpIj4KICAgICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMC43NTEyMjYsIDEuOTg5Mjk5KSI+CiAgICAgICAgPHBhdGggZD0iTS00NDAuOCwwbDQzLjcsMTIwLjFjNC41LDEzLjQsOS41LDI5LjQsMTIuOCw0MS43aDAuOGMzLjctMTIuMiw3LjktMjcuNywxMi44LTQyLjQgbDM5LjctMTE5LjJoMzguNUwtMzQ2LjksMTQ1Yy0yNiw2OS43LTQzLjcsMTA1LjQtNjguNiwxMjcuMmMtMTIuNSwxMS43LTI3LjksMjAtNDQuNiwyMy45bC05LjEtMzEuMSBjMTEuNy0zLjksMjIuNS0xMC4xLDMxLjgtMTguMWMxMy4yLTExLjEsMjMuNy0yNS4yLDMwLjYtNDEuMmMxLjUtMi44LDIuNS01LjcsMi45LTguOGMtMC4zLTMuMy0xLjItNi42LTIuNS05LjdMLTQ4MC4yLDAuMSBoMzkuN0wtNDQwLjgsMEwtNDQwLjgsMHoiLz4KICAgICAgPC9nPgogICAgPC9nPgogICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoODIyLjc0ODEwNCwgMC4wMDAwMDApIj4KICAgICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMS40NjQwNTAsIDAuMzc4OTE0KSI+CiAgICAgICAgPHBhdGggZD0iTS00MTMuNywwdjU4LjNoNTJ2MjguMmgtNTJWMTk2YzAsMjUsNywzOS41LDI3LjMsMzkuNWM3LjEsMC4xLDE0LjItMC43LDIxLjEtMi41IGwxLjcsMjcuN2MtMTAuMywzLjctMjEuMyw1LjQtMzIuMiw1Yy03LjMsMC40LTE0LjYtMC43LTIxLjMtMy40Yy02LjgtMi43LTEyLjktNi44LTE3LjktMTIuMWMtMTAuMy0xMC45LTE0LjEtMjktMTQuMS01Mi45IFY4Ni41aC0zMVY1OC4zaDMxVjkuNkwtNDEzLjcsMEwtNDEzLjcsMHoiLz4KICAgICAgPC9nPgogICAgPC9nPgogICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoOTc0LjQzMzI4NiwgNTMuNDc5NjM4KSI+CiAgICAgIDxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKDAuOTkwMDM0LCAwLjYxMDMzOSkiPgogICAgICAgIDxwYXRoIGQ9Ik0tNDQ1LjgsMTEzYzAuOCw1MCwzMi4yLDcwLjYsNjguNiw3MC42YzE5LDAuNiwzNy45LTMsNTUuMy0xMC41bDYuMiwyNi40IGMtMjAuOSw4LjktNDMuNSwxMy4xLTY2LjIsMTIuNmMtNjEuNSwwLTk4LjMtNDEuMi05OC4zLTEwMi41Qy00ODAuMiw0OC4yLTQ0NC43LDAtMzg2LjUsMGM2NS4yLDAsODIuNyw1OC4zLDgyLjcsOTUuNyBjLTAuMSw1LjgtMC41LDExLjUtMS4yLDE3LjJoLTE0MC42SC00NDUuOEwtNDQ1LjgsMTEzeiBNLTMzOS4yLDg2LjZjMC40LTIzLjUtOS41LTYwLjEtNTAuNC02MC4xIGMtMzYuOCwwLTUyLjgsMzQuNC01NS43LDYwLjFILTMzOS4yTC0zMzkuMiw4Ni42TC0zMzkuMiw4Ni42eiIvPgogICAgICA8L2c+CiAgICA8L2c+CiAgICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxMjAxLjk2MTA1OCwgNTMuNDc5NjM4KSI+CiAgICAgIDxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKDEuMTc5NjQwLCAwLjcwNTA2OCkiPgogICAgICAgIDxwYXRoIGQ9Ik0tNDc4LjYsNjhjMC0yMy45LTAuNC00NC41LTEuNy02My40aDMxLjhsMS4yLDM5LjloMS43YzkuMS0yNy4zLDMxLTQ0LjUsNTUuMy00NC41IGMzLjUtMC4xLDcsMC40LDEwLjMsMS4ydjM0LjhjLTQuMS0wLjktOC4yLTEuMy0xMi40LTEuMmMtMjUuNiwwLTQzLjcsMTkuNy00OC43LDQ3LjRjLTEsNS43LTEuNiwxMS41LTEuNywxNy4ydjEwOC4zaC0zNlY2OCBMLTQ3OC42LDY4eiIvPgogICAgICA8L2c+CiAgICA8L2c+CiAgPC9nPgoKICA8ZyBjbGFzcz0ianAtaWNvbi13YXJuMCIgZmlsbD0iI0YzNzcyNiI+CiAgICA8cGF0aCBkPSJNMTM1Mi4zLDMyNi4yaDM3VjI4aC0zN1YzMjYuMnogTTE2MDQuOCwzMjYuMmMtMi41LTEzLjktMy40LTMxLjEtMy40LTQ4Ljd2LTc2IGMwLTQwLjctMTUuMS04My4xLTc3LjMtODMuMWMtMjUuNiwwLTUwLDcuMS02Ni44LDE4LjFsOC40LDI0LjRjMTQuMy05LjIsMzQtMTUuMSw1My0xNS4xYzQxLjYsMCw0Ni4yLDMwLjIsNDYuMiw0N3Y0LjIgYy03OC42LTAuNC0xMjIuMywyNi41LTEyMi4zLDc1LjZjMCwyOS40LDIxLDU4LjQsNjIuMiw1OC40YzI5LDAsNTAuOS0xNC4zLDYyLjItMzAuMmgxLjNsMi45LDI1LjZIMTYwNC44eiBNMTU2NS43LDI1Ny43IGMwLDMuOC0wLjgsOC0yLjEsMTEuOGMtNS45LDE3LjItMjIuNywzNC00OS4yLDM0Yy0xOC45LDAtMzQuOS0xMS4zLTM0LjktMzUuM2MwLTM5LjUsNDUuOC00Ni42LDg2LjItNDUuOFYyNTcuN3ogTTE2OTguNSwzMjYuMiBsMS43LTMzLjZoMS4zYzE1LjEsMjYuOSwzOC43LDM4LjIsNjguMSwzOC4yYzQ1LjQsMCw5MS4yLTM2LjEsOTEuMi0xMDguOGMwLjQtNjEuNy0zNS4zLTEwMy43LTg1LjctMTAzLjcgYy0zMi44LDAtNTYuMywxNC43LTY5LjMsMzcuNGgtMC44VjI4aC0zNi42djI0NS43YzAsMTguMS0wLjgsMzguNi0xLjcsNTIuNUgxNjk4LjV6IE0xNzA0LjgsMjA4LjJjMC01LjksMS4zLTEwLjksMi4xLTE1LjEgYzcuNi0yOC4xLDMxLjEtNDUuNCw1Ni4zLTQ1LjRjMzkuNSwwLDYwLjUsMzQuOSw2MC41LDc1LjZjMCw0Ni42LTIzLjEsNzguMS02MS44LDc4LjFjLTI2LjksMC00OC4zLTE3LjYtNTUuNS00My4zIGMtMC44LTQuMi0xLjctOC44LTEuNy0xMy40VjIwOC4yeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-kernel: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiIgZmlsbD0iIzYxNjE2MSIgZD0iTTE1IDlIOXY2aDZWOXptLTIgNGgtMnYtMmgydjJ6bTgtMlY5aC0yVjdjMC0xLjEtLjktMi0yLTJoLTJWM2gtMnYyaC0yVjNIOXYySDdjLTEuMSAwLTIgLjktMiAydjJIM3YyaDJ2MkgzdjJoMnYyYzAgMS4xLjkgMiAyIDJoMnYyaDJ2LTJoMnYyaDJ2LTJoMmMxLjEgMCAyLS45IDItMnYtMmgydi0yaC0ydi0yaDJ6bS00IDZIN1Y3aDEwdjEweiIvPgo8L3N2Zz4K);
  --jp-icon-keyboard: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMjAgNUg0Yy0xLjEgMC0xLjk5LjktMS45OSAyTDIgMTdjMCAxLjEuOSAyIDIgMmgxNmMxLjEgMCAyLS45IDItMlY3YzAtMS4xLS45LTItMi0yem0tOSAzaDJ2MmgtMlY4em0wIDNoMnYyaC0ydi0yek04IDhoMnYySDhWOHptMCAzaDJ2Mkg4di0yem0tMSAySDV2LTJoMnYyem0wLTNINVY4aDJ2MnptOSA3SDh2LTJoOHYyem0wLTRoLTJ2LTJoMnYyem0wLTNoLTJWOGgydjJ6bTMgM2gtMnYtMmgydjJ6bTAtM2gtMlY4aDJ2MnoiLz4KPC9zdmc+Cg==);
  --jp-icon-launch: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMzIgMzIiIHdpZHRoPSIzMiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIj4KICAgIDxwYXRoIGQ9Ik0yNiwyOEg2YTIuMDAyNywyLjAwMjcsMCwwLDEtMi0yVjZBMi4wMDI3LDIuMDAyNywwLDAsMSw2LDRIMTZWNkg2VjI2SDI2VjE2aDJWMjZBMi4wMDI3LDIuMDAyNywwLDAsMSwyNiwyOFoiLz4KICAgIDxwb2x5Z29uIHBvaW50cz0iMjAgMiAyMCA0IDI2LjU4NiA0IDE4IDEyLjU4NiAxOS40MTQgMTQgMjggNS40MTQgMjggMTIgMzAgMTIgMzAgMiAyMCAyIi8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-launcher: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMTkgMTlINVY1aDdWM0g1YTIgMiAwIDAwLTIgMnYxNGEyIDIgMCAwMDIgMmgxNGMxLjEgMCAyLS45IDItMnYtN2gtMnY3ek0xNCAzdjJoMy41OWwtOS44MyA5LjgzIDEuNDEgMS40MUwxOSA2LjQxVjEwaDJWM2gtN3oiLz4KPC9zdmc+Cg==);
  --jp-icon-line-form: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxwYXRoIGZpbGw9IndoaXRlIiBkPSJNNS44OCA0LjEyTDEzLjc2IDEybC03Ljg4IDcuODhMOCAyMmwxMC0xMEw4IDJ6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-link: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTMuOSAxMmMwLTEuNzEgMS4zOS0zLjEgMy4xLTMuMWg0VjdIN2MtMi43NiAwLTUgMi4yNC01IDVzMi4yNCA1IDUgNWg0di0xLjlIN2MtMS43MSAwLTMuMS0xLjM5LTMuMS0zLjF6TTggMTNoOHYtMkg4djJ6bTktNmgtNHYxLjloNGMxLjcxIDAgMy4xIDEuMzkgMy4xIDMuMXMtMS4zOSAzLjEtMy4xIDMuMWgtNFYxN2g0YzIuNzYgMCA1LTIuMjQgNS01cy0yLjI0LTUtNS01eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-list: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiM2MTYxNjEiIGQ9Ik0xOSA1djE0SDVWNWgxNG0xLjEtMkgzLjljLS41IDAtLjkuNC0uOS45djE2LjJjMCAuNC40LjkuOS45aDE2LjJjLjQgMCAuOS0uNS45LS45VjMuOWMwLS41LS41LS45LS45LS45ek0xMSA3aDZ2MmgtNlY3em0wIDRoNnYyaC02di0yem0wIDRoNnYyaC02ek03IDdoMnYySDd6bTAgNGgydjJIN3ptMCA0aDJ2Mkg3eiIvPgo8L3N2Zz4K);
  --jp-icon-markdown: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1jb250cmFzdDAganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjN0IxRkEyIiBkPSJNNSAxNC45aDEybC02LjEgNnptOS40LTYuOGMwLTEuMy0uMS0yLjktLjEtNC41LS40IDEuNC0uOSAyLjktMS4zIDQuM2wtMS4zIDQuM2gtMkw4LjUgNy45Yy0uNC0xLjMtLjctMi45LTEtNC4zLS4xIDEuNi0uMSAzLjItLjIgNC42TDcgMTIuNEg0LjhsLjctMTFoMy4zTDEwIDVjLjQgMS4yLjcgMi43IDEgMy45LjMtMS4yLjctMi42IDEtMy45bDEuMi0zLjdoMy4zbC42IDExaC0yLjRsLS4zLTQuMnoiLz4KPC9zdmc+Cg==);
  --jp-icon-move-down: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTQiIGhlaWdodD0iMTQiIHZpZXdCb3g9IjAgMCAxNCAxNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPHBhdGggY2xhc3M9ImpwLWljb24zIiBkPSJNMTIuNDcxIDcuNTI4OTlDMTIuNzYzMiA3LjIzNjg0IDEyLjc2MzIgNi43NjMxNiAxMi40NzEgNi40NzEwMVY2LjQ3MTAxQzEyLjE3OSA2LjE3OTA1IDExLjcwNTcgNi4xNzg4NCAxMS40MTM1IDYuNDcwNTRMNy43NSAxMC4xMjc1VjEuNzVDNy43NSAxLjMzNTc5IDcuNDE0MjEgMSA3IDFWMUM2LjU4NTc5IDEgNi4yNSAxLjMzNTc5IDYuMjUgMS43NVYxMC4xMjc1TDIuNTk3MjYgNi40NjgyMkMyLjMwMzM4IDYuMTczODEgMS44MjY0MSA2LjE3MzU5IDEuNTMyMjYgNi40Njc3NFY2LjQ2Nzc0QzEuMjM4MyA2Ljc2MTcgMS4yMzgzIDcuMjM4MyAxLjUzMjI2IDcuNTMyMjZMNi4yOTI4OSAxMi4yOTI5QzYuNjgzNDIgMTIuNjgzNCA3LjMxNjU4IDEyLjY4MzQgNy43MDcxMSAxMi4yOTI5TDEyLjQ3MSA3LjUyODk5WiIgZmlsbD0iIzYxNjE2MSIvPgo8L3N2Zz4K);
  --jp-icon-move-up: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTQiIGhlaWdodD0iMTQiIHZpZXdCb3g9IjAgMCAxNCAxNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPHBhdGggY2xhc3M9ImpwLWljb24zIiBkPSJNMS41Mjg5OSA2LjQ3MTAxQzEuMjM2ODQgNi43NjMxNiAxLjIzNjg0IDcuMjM2ODQgMS41Mjg5OSA3LjUyODk5VjcuNTI4OTlDMS44MjA5NSA3LjgyMDk1IDIuMjk0MjYgNy44MjExNiAyLjU4NjQ5IDcuNTI5NDZMNi4yNSAzLjg3MjVWMTIuMjVDNi4yNSAxMi42NjQyIDYuNTg1NzkgMTMgNyAxM1YxM0M3LjQxNDIxIDEzIDcuNzUgMTIuNjY0MiA3Ljc1IDEyLjI1VjMuODcyNUwxMS40MDI3IDcuNTMxNzhDMTEuNjk2NiA3LjgyNjE5IDEyLjE3MzYgNy44MjY0MSAxMi40Njc3IDcuNTMyMjZWNy41MzIyNkMxMi43NjE3IDcuMjM4MyAxMi43NjE3IDYuNzYxNyAxMi40Njc3IDYuNDY3NzRMNy43MDcxMSAxLjcwNzExQzcuMzE2NTggMS4zMTY1OCA2LjY4MzQyIDEuMzE2NTggNi4yOTI4OSAxLjcwNzExTDEuNTI4OTkgNi40NzEwMVoiIGZpbGw9IiM2MTYxNjEiLz4KPC9zdmc+Cg==);
  --jp-icon-new-folder: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTIwIDZoLThsLTItMkg0Yy0xLjExIDAtMS45OS44OS0xLjk5IDJMMiAxOGMwIDEuMTEuODkgMiAyIDJoMTZjMS4xMSAwIDItLjg5IDItMlY4YzAtMS4xMS0uODktMi0yLTJ6bS0xIDhoLTN2M2gtMnYtM2gtM3YtMmgzVjloMnYzaDN2MnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-not-trusted: url(data:image/svg+xml;base64,PHN2ZyBmaWxsPSJub25lIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI1IDI1Ij4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiIgc3Ryb2tlPSIjMzMzMzMzIiBzdHJva2Utd2lkdGg9IjIiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDMgMykiIGQ9Ik0xLjg2MDk0IDExLjQ0MDlDMC44MjY0NDggOC43NzAyNyAwLjg2Mzc3OSA2LjA1NzY0IDEuMjQ5MDcgNC4xOTkzMkMyLjQ4MjA2IDMuOTMzNDcgNC4wODA2OCAzLjQwMzQ3IDUuNjAxMDIgMi44NDQ5QzcuMjM1NDkgMi4yNDQ0IDguODU2NjYgMS41ODE1IDkuOTg3NiAxLjA5NTM5QzExLjA1OTcgMS41ODM0MSAxMi42MDk0IDIuMjQ0NCAxNC4yMTggMi44NDMzOUMxNS43NTAzIDMuNDEzOTQgMTcuMzk5NSAzLjk1MjU4IDE4Ljc1MzkgNC4yMTM4NUMxOS4xMzY0IDYuMDcxNzcgMTkuMTcwOSA4Ljc3NzIyIDE4LjEzOSAxMS40NDA5QzE3LjAzMDMgMTQuMzAzMiAxNC42NjY4IDE3LjE4NDQgOS45OTk5OSAxOC45MzU0QzUuMzMzMTkgMTcuMTg0NCAyLjk2OTY4IDE0LjMwMzIgMS44NjA5NCAxMS40NDA5WiIvPgogICAgPHBhdGggY2xhc3M9ImpwLWljb24yIiBzdHJva2U9IiMzMzMzMzMiIHN0cm9rZS13aWR0aD0iMiIgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoOS4zMTU5MiA5LjMyMDMxKSIgZD0iTTcuMzY4NDIgMEwwIDcuMzY0NzkiLz4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiIgc3Ryb2tlPSIjMzMzMzMzIiBzdHJva2Utd2lkdGg9IjIiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDkuMzE1OTIgMTYuNjgzNikgc2NhbGUoMSAtMSkiIGQ9Ik03LjM2ODQyIDBMMCA3LjM2NDc5Ii8+Cjwvc3ZnPgo=);
  --jp-icon-notebook: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8ZyBjbGFzcz0ianAtbm90ZWJvb2staWNvbi1jb2xvciBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiNFRjZDMDAiPgogICAgPHBhdGggZD0iTTE4LjcgMy4zdjE1LjRIMy4zVjMuM2gxNS40bTEuNS0xLjVIMS44djE4LjNoMTguM2wuMS0xOC4zeiIvPgogICAgPHBhdGggZD0iTTE2LjUgMTYuNWwtNS40LTQuMy01LjYgNC4zdi0xMWgxMXoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-numbering: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjIiIGhlaWdodD0iMjIiIHZpZXdCb3g9IjAgMCAyOCAyOCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CgkJPHBhdGggZD0iTTQgMTlINlYxOS41SDVWMjAuNUg2VjIxSDRWMjJIN1YxOEg0VjE5Wk01IDEwSDZWNkg0VjdINVYxMFpNNCAxM0g1LjhMNCAxNS4xVjE2SDdWMTVINS4yTDcgMTIuOVYxMkg0VjEzWk05IDdWOUgyM1Y3SDlaTTkgMjFIMjNWMTlIOVYyMVpNOSAxNUgyM1YxM0g5VjE1WiIvPgoJPC9nPgo8L3N2Zz4K);
  --jp-icon-offline-bolt: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCIgd2lkdGg9IjE2Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEyIDIuMDJjLTUuNTEgMC05Ljk4IDQuNDctOS45OCA5Ljk4czQuNDcgOS45OCA5Ljk4IDkuOTggOS45OC00LjQ3IDkuOTgtOS45OFMxNy41MSAyLjAyIDEyIDIuMDJ6TTExLjQ4IDIwdi02LjI2SDhMMTMgNHY2LjI2aDMuMzVMMTEuNDggMjB6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-palette: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTE4IDEzVjIwSDRWNkg5LjAyQzkuMDcgNS4yOSA5LjI0IDQuNjIgOS41IDRINEMyLjkgNCAyIDQuOSAyIDZWMjBDMiAyMS4xIDIuOSAyMiA0IDIySDE4QzE5LjEgMjIgMjAgMjEuMSAyMCAyMFYxNUwxOCAxM1pNMTkuMyA4Ljg5QzE5Ljc0IDguMTkgMjAgNy4zOCAyMCA2LjVDMjAgNC4wMSAxNy45OSAyIDE1LjUgMkMxMy4wMSAyIDExIDQuMDEgMTEgNi41QzExIDguOTkgMTMuMDEgMTEgMTUuNDkgMTFDMTYuMzcgMTEgMTcuMTkgMTAuNzQgMTcuODggMTAuM0wyMSAxMy40MkwyMi40MiAxMkwxOS4zIDguODlaTTE1LjUgOUMxNC4xMiA5IDEzIDcuODggMTMgNi41QzEzIDUuMTIgMTQuMTIgNCAxNS41IDRDMTYuODggNCAxOCA1LjEyIDE4IDYuNUMxOCA3Ljg4IDE2Ljg4IDkgMTUuNSA5WiIvPgogICAgPHBhdGggZmlsbC1ydWxlPSJldmVub2RkIiBjbGlwLXJ1bGU9ImV2ZW5vZGQiIGQ9Ik00IDZIOS4wMTg5NEM5LjAwNjM5IDYuMTY1MDIgOSA2LjMzMTc2IDkgNi41QzkgOC44MTU3NyAxMC4yMTEgMTAuODQ4NyAxMi4wMzQzIDEySDlWMTRIMTZWMTIuOTgxMUMxNi41NzAzIDEyLjkzNzcgMTcuMTIgMTIuODIwNyAxNy42Mzk2IDEyLjYzOTZMMTggMTNWMjBINFY2Wk04IDhINlYxMEg4VjhaTTYgMTJIOFYxNEg2VjEyWk04IDE2SDZWMThIOFYxNlpNOSAxNkgxNlYxOEg5VjE2WiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-paste: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTE5IDJoLTQuMThDMTQuNC44NCAxMy4zIDAgMTIgMGMtMS4zIDAtMi40Ljg0LTIuODIgMkg1Yy0xLjEgMC0yIC45LTIgMnYxNmMwIDEuMS45IDIgMiAyaDE0YzEuMSAwIDItLjkgMi0yVjRjMC0xLjEtLjktMi0yLTJ6bS03IDBjLjU1IDAgMSAuNDUgMSAxcy0uNDUgMS0xIDEtMS0uNDUtMS0xIC40NS0xIDEtMXptNyAxOEg1VjRoMnYzaDEwVjRoMnYxNnoiLz4KICAgIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-pdf: url(data:image/svg+xml;base64,PHN2ZwogICB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyMiAyMiIgd2lkdGg9IjE2Ij4KICAgIDxwYXRoIHRyYW5zZm9ybT0icm90YXRlKDQ1KSIgY2xhc3M9ImpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iI0ZGMkEyQSIKICAgICAgIGQ9Im0gMjIuMzQ0MzY5LC0zLjAxNjM2NDIgaCA1LjYzODYwNCB2IDEuNTc5MjQzMyBoIC0zLjU0OTIyNyB2IDEuNTA4NjkyOTkgaCAzLjMzNzU3NiBWIDEuNjUwODE1NCBoIC0zLjMzNzU3NiB2IDMuNDM1MjYxMyBoIC0yLjA4OTM3NyB6IG0gLTcuMTM2NDQ0LDEuNTc5MjQzMyB2IDQuOTQzOTU0MyBoIDAuNzQ4OTIgcSAxLjI4MDc2MSwwIDEuOTUzNzAzLC0wLjYzNDk1MzUgMC42NzgzNjksLTAuNjM0OTUzNSAwLjY3ODM2OSwtMS44NDUxNjQxIDAsLTEuMjA0NzgzNTUgLTAuNjcyOTQyLC0xLjgzNDMxMDExIC0wLjY3Mjk0MiwtMC42Mjk1MjY1OSAtMS45NTkxMywtMC42Mjk1MjY1OSB6IG0gLTIuMDg5Mzc3LC0xLjU3OTI0MzMgaCAyLjIwMzM0MyBxIDEuODQ1MTY0LDAgMi43NDYwMzksMC4yNjU5MjA3IDAuOTA2MzAxLDAuMjYwNDkzNyAxLjU1MjEwOCwwLjg5MDAyMDMgMC41Njk4MywwLjU0ODEyMjMgMC44NDY2MDUsMS4yNjQ0ODAwNiAwLjI3Njc3NCwwLjcxNjM1NzgxIDAuMjc2Nzc0LDEuNjIyNjU4OTQgMCwwLjkxNzE1NTEgLTAuMjc2Nzc0LDEuNjM4OTM5OSAtMC4yNzY3NzUsMC43MTYzNTc4IC0wLjg0NjYwNSwxLjI2NDQ4IC0wLjY1MTIzNCwwLjYyOTUyNjYgLTEuNTYyOTYyLDAuODk1NDQ3MyAtMC45MTE3MjgsMC4yNjA0OTM3IC0yLjczNTE4NSwwLjI2MDQ5MzcgaCAtMi4yMDMzNDMgeiBtIC04LjE0NTg1NjUsMCBoIDMuNDY3ODIzIHEgMS41NDY2ODE2LDAgMi4zNzE1Nzg1LDAuNjg5MjIzIDAuODMwMzI0LDAuNjgzNzk2MSAwLjgzMDMyNCwxLjk1MzcwMzE0IDAsMS4yNzUzMzM5NyAtMC44MzAzMjQsMS45NjQ1NTcwNiBRIDkuOTg3MTk2MSwyLjI3NDkxNSA4LjQ0MDUxNDUsMi4yNzQ5MTUgSCA3LjA2MjA2ODQgViA1LjA4NjA3NjcgSCA0Ljk3MjY5MTUgWiBtIDIuMDg5Mzc2OSwxLjUxNDExOTkgdiAyLjI2MzAzOTQzIGggMS4xNTU5NDEgcSAwLjYwNzgxODgsMCAwLjkzODg2MjksLTAuMjkzMDU1NDcgMC4zMzEwNDQxLC0wLjI5ODQ4MjQxIDAuMzMxMDQ0MSwtMC44NDExNzc3MiAwLC0wLjU0MjY5NTMxIC0wLjMzMTA0NDEsLTAuODM1NzUwNzQgLTAuMzMxMDQ0MSwtMC4yOTMwNTU1IC0wLjkzODg2MjksLTAuMjkzMDU1NSB6IgovPgo8L3N2Zz4K);
  --jp-icon-python: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iLTEwIC0xMCAxMzEuMTYxMzYxNjk0MzM1OTQgMTMyLjM4ODk5OTkzODk2NDg0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjMzA2OTk4IiBkPSJNIDU0LjkxODc4NSw5LjE5Mjc0MjFlLTQgQyA1MC4zMzUxMzIsMC4wMjIyMTcyNyA0NS45NTc4NDYsMC40MTMxMzY5NyA0Mi4xMDYyODUsMS4wOTQ2NjkzIDMwLjc2MDA2OSwzLjA5OTE3MzEgMjguNzAwMDM2LDcuMjk0NzcxNCAyOC43MDAwMzUsMTUuMDMyMTY5IHYgMTAuMjE4NzUgaCAyNi44MTI1IHYgMy40MDYyNSBoIC0yNi44MTI1IC0xMC4wNjI1IGMgLTcuNzkyNDU5LDAgLTE0LjYxNTc1ODgsNC42ODM3MTcgLTE2Ljc0OTk5OTgsMTMuNTkzNzUgLTIuNDYxODE5OTgsMTAuMjEyOTY2IC0yLjU3MTAxNTA4LDE2LjU4NjAyMyAwLDI3LjI1IDEuOTA1OTI4Myw3LjkzNzg1MiA2LjQ1NzU0MzIsMTMuNTkzNzQ4IDE0LjI0OTk5OTgsMTMuNTkzNzUgaCA5LjIxODc1IHYgLTEyLjI1IGMgMCwtOC44NDk5MDIgNy42NTcxNDQsLTE2LjY1NjI0OCAxNi43NSwtMTYuNjU2MjUgaCAyNi43ODEyNSBjIDcuNDU0OTUxLDAgMTMuNDA2MjUzLC02LjEzODE2NCAxMy40MDYyNSwtMTMuNjI1IHYgLTI1LjUzMTI1IGMgMCwtNy4yNjYzMzg2IC02LjEyOTk4LC0xMi43MjQ3NzcxIC0xMy40MDYyNSwtMTMuOTM3NDk5NyBDIDY0LjI4MTU0OCwwLjMyNzk0Mzk3IDU5LjUwMjQzOCwtMC4wMjAzNzkwMyA1NC45MTg3ODUsOS4xOTI3NDIxZS00IFogbSAtMTQuNSw4LjIxODc1MDEyNTc5IGMgMi43Njk1NDcsMCA1LjAzMTI1LDIuMjk4NjQ1NiA1LjAzMTI1LDUuMTI0OTk5NiAtMmUtNiwyLjgxNjMzNiAtMi4yNjE3MDMsNS4wOTM3NSAtNS4wMzEyNSw1LjA5Mzc1IC0yLjc3OTQ3NiwtMWUtNiAtNS4wMzEyNSwtMi4yNzc0MTUgLTUuMDMxMjUsLTUuMDkzNzUgLTEwZS03LC0yLjgyNjM1MyAyLjI1MTc3NCwtNS4xMjQ5OTk2IDUuMDMxMjUsLTUuMTI0OTk5NiB6Ii8+CiAgPHBhdGggY2xhc3M9ImpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iI2ZmZDQzYiIgZD0ibSA4NS42Mzc1MzUsMjguNjU3MTY5IHYgMTEuOTA2MjUgYyAwLDkuMjMwNzU1IC03LjgyNTg5NSwxNi45OTk5OTkgLTE2Ljc1LDE3IGggLTI2Ljc4MTI1IGMgLTcuMzM1ODMzLDAgLTEzLjQwNjI0OSw2LjI3ODQ4MyAtMTMuNDA2MjUsMTMuNjI1IHYgMjUuNTMxMjQ3IGMgMCw3LjI2NjM0NCA2LjMxODU4OCwxMS41NDAzMjQgMTMuNDA2MjUsMTMuNjI1MDA0IDguNDg3MzMxLDIuNDk1NjEgMTYuNjI2MjM3LDIuOTQ2NjMgMjYuNzgxMjUsMCA2Ljc1MDE1NSwtMS45NTQzOSAxMy40MDYyNTMsLTUuODg3NjEgMTMuNDA2MjUsLTEzLjYyNTAwNCBWIDg2LjUwMDkxOSBoIC0yNi43ODEyNSB2IC0zLjQwNjI1IGggMjYuNzgxMjUgMTMuNDA2MjU0IGMgNy43OTI0NjEsMCAxMC42OTYyNTEsLTUuNDM1NDA4IDEzLjQwNjI0MSwtMTMuNTkzNzUgMi43OTkzMywtOC4zOTg4ODYgMi42ODAyMiwtMTYuNDc1Nzc2IDAsLTI3LjI1IC0xLjkyNTc4LC03Ljc1NzQ0MSAtNS42MDM4NywtMTMuNTkzNzUgLTEzLjQwNjI0MSwtMTMuNTkzNzUgeiBtIC0xNS4wNjI1LDY0LjY1NjI1IGMgMi43Nzk0NzgsM2UtNiA1LjAzMTI1LDIuMjc3NDE3IDUuMDMxMjUsNS4wOTM3NDcgLTJlLTYsMi44MjYzNTQgLTIuMjUxNzc1LDUuMTI1MDA0IC01LjAzMTI1LDUuMTI1MDA0IC0yLjc2OTU1LDAgLTUuMDMxMjUsLTIuMjk4NjUgLTUuMDMxMjUsLTUuMTI1MDA0IDJlLTYsLTIuODE2MzMgMi4yNjE2OTcsLTUuMDkzNzQ3IDUuMDMxMjUsLTUuMDkzNzQ3IHoiLz4KPC9zdmc+Cg==);
  --jp-icon-r-kernel: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1jb250cmFzdDMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjMjE5NkYzIiBkPSJNNC40IDIuNWMxLjItLjEgMi45LS4zIDQuOS0uMyAyLjUgMCA0LjEuNCA1LjIgMS4zIDEgLjcgMS41IDEuOSAxLjUgMy41IDAgMi0xLjQgMy41LTIuOSA0LjEgMS4yLjQgMS43IDEuNiAyLjIgMyAuNiAxLjkgMSAzLjkgMS4zIDQuNmgtMy44Yy0uMy0uNC0uOC0xLjctMS4yLTMuN3MtMS4yLTIuNi0yLjYtMi42aC0uOXY2LjRINC40VjIuNXptMy43IDYuOWgxLjRjMS45IDAgMi45LS45IDIuOS0yLjNzLTEtMi4zLTIuOC0yLjNjLS43IDAtMS4zIDAtMS42LjJ2NC41aC4xdi0uMXoiLz4KPC9zdmc+Cg==);
  --jp-icon-react: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMTUwIDE1MCA1NDEuOSAyOTUuMyI+CiAgPGcgY2xhc3M9ImpwLWljb24tYnJhbmQyIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iIzYxREFGQiI+CiAgICA8cGF0aCBkPSJNNjY2LjMgMjk2LjVjMC0zMi41LTQwLjctNjMuMy0xMDMuMS04Mi40IDE0LjQtNjMuNiA4LTExNC4yLTIwLjItMTMwLjQtNi41LTMuOC0xNC4xLTUuNi0yMi40LTUuNnYyMi4zYzQuNiAwIDguMy45IDExLjQgMi42IDEzLjYgNy44IDE5LjUgMzcuNSAxNC45IDc1LjctMS4xIDkuNC0yLjkgMTkuMy01LjEgMjkuNC0xOS42LTQuOC00MS04LjUtNjMuNS0xMC45LTEzLjUtMTguNS0yNy41LTM1LjMtNDEuNi01MCAzMi42LTMwLjMgNjMuMi00Ni45IDg0LTQ2LjlWNzhjLTI3LjUgMC02My41IDE5LjYtOTkuOSA1My42LTM2LjQtMzMuOC03Mi40LTUzLjItOTkuOS01My4ydjIyLjNjMjAuNyAwIDUxLjQgMTYuNSA4NCA0Ni42LTE0IDE0LjctMjggMzEuNC00MS4zIDQ5LjktMjIuNiAyLjQtNDQgNi4xLTYzLjYgMTEtMi4zLTEwLTQtMTkuNy01LjItMjktNC43LTM4LjIgMS4xLTY3LjkgMTQuNi03NS44IDMtMS44IDYuOS0yLjYgMTEuNS0yLjZWNzguNWMtOC40IDAtMTYgMS44LTIyLjYgNS42LTI4LjEgMTYuMi0zNC40IDY2LjctMTkuOSAxMzAuMS02Mi4yIDE5LjItMTAyLjcgNDkuOS0xMDIuNyA4Mi4zIDAgMzIuNSA0MC43IDYzLjMgMTAzLjEgODIuNC0xNC40IDYzLjYtOCAxMTQuMiAyMC4yIDEzMC40IDYuNSAzLjggMTQuMSA1LjYgMjIuNSA1LjYgMjcuNSAwIDYzLjUtMTkuNiA5OS45LTUzLjYgMzYuNCAzMy44IDcyLjQgNTMuMiA5OS45IDUzLjIgOC40IDAgMTYtMS44IDIyLjYtNS42IDI4LjEtMTYuMiAzNC40LTY2LjcgMTkuOS0xMzAuMSA2Mi0xOS4xIDEwMi41LTQ5LjkgMTAyLjUtODIuM3ptLTEzMC4yLTY2LjdjLTMuNyAxMi45LTguMyAyNi4yLTEzLjUgMzkuNS00LjEtOC04LjQtMTYtMTMuMS0yNC00LjYtOC05LjUtMTUuOC0xNC40LTIzLjQgMTQuMiAyLjEgMjcuOSA0LjcgNDEgNy45em0tNDUuOCAxMDYuNWMtNy44IDEzLjUtMTUuOCAyNi4zLTI0LjEgMzguMi0xNC45IDEuMy0zMCAyLTQ1LjIgMi0xNS4xIDAtMzAuMi0uNy00NS0xLjktOC4zLTExLjktMTYuNC0yNC42LTI0LjItMzgtNy42LTEzLjEtMTQuNS0yNi40LTIwLjgtMzkuOCA2LjItMTMuNCAxMy4yLTI2LjggMjAuNy0zOS45IDcuOC0xMy41IDE1LjgtMjYuMyAyNC4xLTM4LjIgMTQuOS0xLjMgMzAtMiA0NS4yLTIgMTUuMSAwIDMwLjIuNyA0NSAxLjkgOC4zIDExLjkgMTYuNCAyNC42IDI0LjIgMzggNy42IDEzLjEgMTQuNSAyNi40IDIwLjggMzkuOC02LjMgMTMuNC0xMy4yIDI2LjgtMjAuNyAzOS45em0zMi4zLTEzYzUuNCAxMy40IDEwIDI2LjggMTMuOCAzOS44LTEzLjEgMy4yLTI2LjkgNS45LTQxLjIgOCA0LjktNy43IDkuOC0xNS42IDE0LjQtMjMuNyA0LjYtOCA4LjktMTYuMSAxMy0yNC4xek00MjEuMiA0MzBjLTkuMy05LjYtMTguNi0yMC4zLTI3LjgtMzIgOSAuNCAxOC4yLjcgMjcuNS43IDkuNCAwIDE4LjctLjIgMjcuOC0uNy05IDExLjctMTguMyAyMi40LTI3LjUgMzJ6bS03NC40LTU4LjljLTE0LjItMi4xLTI3LjktNC43LTQxLTcuOSAzLjctMTIuOSA4LjMtMjYuMiAxMy41LTM5LjUgNC4xIDggOC40IDE2IDEzLjEgMjQgNC43IDggOS41IDE1LjggMTQuNCAyMy40ek00MjAuNyAxNjNjOS4zIDkuNiAxOC42IDIwLjMgMjcuOCAzMi05LS40LTE4LjItLjctMjcuNS0uNy05LjQgMC0xOC43LjItMjcuOC43IDktMTEuNyAxOC4zLTIyLjQgMjcuNS0zMnptLTc0IDU4LjljLTQuOSA3LjctOS44IDE1LjYtMTQuNCAyMy43LTQuNiA4LTguOSAxNi0xMyAyNC01LjQtMTMuNC0xMC0yNi44LTEzLjgtMzkuOCAxMy4xLTMuMSAyNi45LTUuOCA0MS4yLTcuOXptLTkwLjUgMTI1LjJjLTM1LjQtMTUuMS01OC4zLTM0LjktNTguMy01MC42IDAtMTUuNyAyMi45LTM1LjYgNTguMy01MC42IDguNi0zLjcgMTgtNyAyNy43LTEwLjEgNS43IDE5LjYgMTMuMiA0MCAyMi41IDYwLjktOS4yIDIwLjgtMTYuNiA0MS4xLTIyLjIgNjAuNi05LjktMy4xLTE5LjMtNi41LTI4LTEwLjJ6TTMxMCA0OTBjLTEzLjYtNy44LTE5LjUtMzcuNS0xNC45LTc1LjcgMS4xLTkuNCAyLjktMTkuMyA1LjEtMjkuNCAxOS42IDQuOCA0MSA4LjUgNjMuNSAxMC45IDEzLjUgMTguNSAyNy41IDM1LjMgNDEuNiA1MC0zMi42IDMwLjMtNjMuMiA0Ni45LTg0IDQ2LjktNC41LS4xLTguMy0xLTExLjMtMi43em0yMzcuMi03Ni4yYzQuNyAzOC4yLTEuMSA2Ny45LTE0LjYgNzUuOC0zIDEuOC02LjkgMi42LTExLjUgMi42LTIwLjcgMC01MS40LTE2LjUtODQtNDYuNiAxNC0xNC43IDI4LTMxLjQgNDEuMy00OS45IDIyLjYtMi40IDQ0LTYuMSA2My42LTExIDIuMyAxMC4xIDQuMSAxOS44IDUuMiAyOS4xem0zOC41LTY2LjdjLTguNiAzLjctMTggNy0yNy43IDEwLjEtNS43LTE5LjYtMTMuMi00MC0yMi41LTYwLjkgOS4yLTIwLjggMTYuNi00MS4xIDIyLjItNjAuNiA5LjkgMy4xIDE5LjMgNi41IDI4LjEgMTAuMiAzNS40IDE1LjEgNTguMyAzNC45IDU4LjMgNTAuNi0uMSAxNS43LTIzIDM1LjYtNTguNCA1MC42ek0zMjAuOCA3OC40eiIvPgogICAgPGNpcmNsZSBjeD0iNDIwLjkiIGN5PSIyOTYuNSIgcj0iNDUuNyIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-redo: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIGhlaWdodD0iMjQiIHZpZXdCb3g9IjAgMCAyNCAyNCIgd2lkdGg9IjE2Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgICA8cGF0aCBkPSJNMCAwaDI0djI0SDB6IiBmaWxsPSJub25lIi8+PHBhdGggZD0iTTE4LjQgMTAuNkMxNi41NSA4Ljk5IDE0LjE1IDggMTEuNSA4Yy00LjY1IDAtOC41OCAzLjAzLTkuOTYgNy4yMkwzLjkgMTZjMS4wNS0zLjE5IDQuMDUtNS41IDcuNi01LjUgMS45NSAwIDMuNzMuNzIgNS4xMiAxLjg4TDEzIDE2aDlWN2wtMy42IDMuNnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-refresh: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTkgMTMuNWMtMi40OSAwLTQuNS0yLjAxLTQuNS00LjVTNi41MSA0LjUgOSA0LjVjMS4yNCAwIDIuMzYuNTIgMy4xNyAxLjMzTDEwIDhoNVYzbC0xLjc2IDEuNzZDMTIuMTUgMy42OCAxMC42NiAzIDkgMyA1LjY5IDMgMy4wMSA1LjY5IDMuMDEgOVM1LjY5IDE1IDkgMTVjMi45NyAwIDUuNDMtMi4xNiA1LjktNWgtMS41MmMtLjQ2IDItMi4yNCAzLjUtNC4zOCAzLjV6Ii8+CiAgICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-regex: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwIDIwIj4KICA8ZyBjbGFzcz0ianAtaWNvbjIiIGZpbGw9IiM0MTQxNDEiPgogICAgPHJlY3QgeD0iMiIgeT0iMiIgd2lkdGg9IjE2IiBoZWlnaHQ9IjE2Ii8+CiAgPC9nPgoKICA8ZyBjbGFzcz0ianAtaWNvbi1hY2NlbnQyIiBmaWxsPSIjRkZGIj4KICAgIDxjaXJjbGUgY2xhc3M9InN0MiIgY3g9IjUuNSIgY3k9IjE0LjUiIHI9IjEuNSIvPgogICAgPHJlY3QgeD0iMTIiIHk9IjQiIGNsYXNzPSJzdDIiIHdpZHRoPSIxIiBoZWlnaHQ9IjgiLz4KICAgIDxyZWN0IHg9IjguNSIgeT0iNy41IiB0cmFuc2Zvcm09Im1hdHJpeCgwLjg2NiAtMC41IDAuNSAwLjg2NiAtMi4zMjU1IDcuMzIxOSkiIGNsYXNzPSJzdDIiIHdpZHRoPSI4IiBoZWlnaHQ9IjEiLz4KICAgIDxyZWN0IHg9IjEyIiB5PSI0IiB0cmFuc2Zvcm09Im1hdHJpeCgwLjUgLTAuODY2IDAuODY2IDAuNSAtMC42Nzc5IDE0LjgyNTIpIiBjbGFzcz0ic3QyIiB3aWR0aD0iMSIgaGVpZ2h0PSI4Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-run: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTggNXYxNGwxMS03eiIvPgogICAgPC9nPgo8L3N2Zz4K);
  --jp-icon-running: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDUxMiA1MTIiPgogIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICA8cGF0aCBkPSJNMjU2IDhDMTE5IDggOCAxMTkgOCAyNTZzMTExIDI0OCAyNDggMjQ4IDI0OC0xMTEgMjQ4LTI0OFMzOTMgOCAyNTYgOHptOTYgMzI4YzAgOC44LTcuMiAxNi0xNiAxNkgxNzZjLTguOCAwLTE2LTcuMi0xNi0xNlYxNzZjMC04LjggNy4yLTE2IDE2LTE2aDE2MGM4LjggMCAxNiA3LjIgMTYgMTZ2MTYweiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-save: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTE3IDNINWMtMS4xMSAwLTIgLjktMiAydjE0YzAgMS4xLjg5IDIgMiAyaDE0YzEuMSAwIDItLjkgMi0yVjdsLTQtNHptLTUgMTZjLTEuNjYgMC0zLTEuMzQtMy0zczEuMzQtMyAzLTMgMyAxLjM0IDMgMy0xLjM0IDMtMyAzem0zLTEwSDVWNWgxMHY0eiIvPgogICAgPC9nPgo8L3N2Zz4K);
  --jp-icon-search: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMTggMTgiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEyLjEsMTAuOWgtMC43bC0wLjItMC4yYzAuOC0wLjksMS4zLTIuMiwxLjMtMy41YzAtMy0yLjQtNS40LTUuNC01LjRTMS44LDQuMiwxLjgsNy4xczIuNCw1LjQsNS40LDUuNCBjMS4zLDAsMi41LTAuNSwzLjUtMS4zbDAuMiwwLjJ2MC43bDQuMSw0LjFsMS4yLTEuMkwxMi4xLDEwLjl6IE03LjEsMTAuOWMtMi4xLDAtMy43LTEuNy0zLjctMy43czEuNy0zLjcsMy43LTMuN3MzLjcsMS43LDMuNywzLjcgUzkuMiwxMC45LDcuMSwxMC45eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-settings: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMTkuNDMgMTIuOThjLjA0LS4zMi4wNy0uNjQuMDctLjk4cy0uMDMtLjY2LS4wNy0uOThsMi4xMS0xLjY1Yy4xOS0uMTUuMjQtLjQyLjEyLS42NGwtMi0zLjQ2Yy0uMTItLjIyLS4zOS0uMy0uNjEtLjIybC0yLjQ5IDFjLS41Mi0uNC0xLjA4LS43My0xLjY5LS45OGwtLjM4LTIuNjVBLjQ4OC40ODggMCAwMDE0IDJoLTRjLS4yNSAwLS40Ni4xOC0uNDkuNDJsLS4zOCAyLjY1Yy0uNjEuMjUtMS4xNy41OS0xLjY5Ljk4bC0yLjQ5LTFjLS4yMy0uMDktLjQ5IDAtLjYxLjIybC0yIDMuNDZjLS4xMy4yMi0uMDcuNDkuMTIuNjRsMi4xMSAxLjY1Yy0uMDQuMzItLjA3LjY1LS4wNy45OHMuMDMuNjYuMDcuOThsLTIuMTEgMS42NWMtLjE5LjE1LS4yNC40Mi0uMTIuNjRsMiAzLjQ2Yy4xMi4yMi4zOS4zLjYxLjIybDIuNDktMWMuNTIuNCAxLjA4LjczIDEuNjkuOThsLjM4IDIuNjVjLjAzLjI0LjI0LjQyLjQ5LjQyaDRjLjI1IDAgLjQ2LS4xOC40OS0uNDJsLjM4LTIuNjVjLjYxLS4yNSAxLjE3LS41OSAxLjY5LS45OGwyLjQ5IDFjLjIzLjA5LjQ5IDAgLjYxLS4yMmwyLTMuNDZjLjEyLS4yMi4wNy0uNDktLjEyLS42NGwtMi4xMS0xLjY1ek0xMiAxNS41Yy0xLjkzIDAtMy41LTEuNTctMy41LTMuNXMxLjU3LTMuNSAzLjUtMy41IDMuNSAxLjU3IDMuNSAzLjUtMS41NyAzLjUtMy41IDMuNXoiLz4KPC9zdmc+Cg==);
  --jp-icon-share: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTYiIHZpZXdCb3g9IjAgMCAyNCAyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTSAxOCAyIEMgMTYuMzU0OTkgMiAxNSAzLjM1NDk5MDQgMTUgNSBDIDE1IDUuMTkwOTUyOSAxNS4wMjE3OTEgNS4zNzcxMjI0IDE1LjA1NjY0MSA1LjU1ODU5MzggTCA3LjkyMTg3NSA5LjcyMDcwMzEgQyA3LjM5ODUzOTkgOS4yNzc4NTM5IDYuNzMyMDc3MSA5IDYgOSBDIDQuMzU0OTkwNCA5IDMgMTAuMzU0OTkgMyAxMiBDIDMgMTMuNjQ1MDEgNC4zNTQ5OTA0IDE1IDYgMTUgQyA2LjczMjA3NzEgMTUgNy4zOTg1Mzk5IDE0LjcyMjE0NiA3LjkyMTg3NSAxNC4yNzkyOTcgTCAxNS4wNTY2NDEgMTguNDM5NDUzIEMgMTUuMDIxNTU1IDE4LjYyMTUxNCAxNSAxOC44MDgzODYgMTUgMTkgQyAxNSAyMC42NDUwMSAxNi4zNTQ5OSAyMiAxOCAyMiBDIDE5LjY0NTAxIDIyIDIxIDIwLjY0NTAxIDIxIDE5IEMgMjEgMTcuMzU0OTkgMTkuNjQ1MDEgMTYgMTggMTYgQyAxNy4yNjc0OCAxNiAxNi42MDE1OTMgMTYuMjc5MzI4IDE2LjA3ODEyNSAxNi43MjI2NTYgTCA4Ljk0MzM1OTQgMTIuNTU4NTk0IEMgOC45NzgyMDk1IDEyLjM3NzEyMiA5IDEyLjE5MDk1MyA5IDEyIEMgOSAxMS44MDkwNDcgOC45NzgyMDk1IDExLjYyMjg3OCA4Ljk0MzM1OTQgMTEuNDQxNDA2IEwgMTYuMDc4MTI1IDcuMjc5Mjk2OSBDIDE2LjYwMTQ2IDcuNzIyMTQ2MSAxNy4yNjc5MjMgOCAxOCA4IEMgMTkuNjQ1MDEgOCAyMSA2LjY0NTAwOTYgMjEgNSBDIDIxIDMuMzU0OTkwNCAxOS42NDUwMSAyIDE4IDIgeiBNIDE4IDQgQyAxOC41NjQxMjkgNCAxOSA0LjQzNTg3MDYgMTkgNSBDIDE5IDUuNTY0MTI5NCAxOC41NjQxMjkgNiAxOCA2IEMgMTcuNDM1ODcxIDYgMTcgNS41NjQxMjk0IDE3IDUgQyAxNyA0LjQzNTg3MDYgMTcuNDM1ODcxIDQgMTggNCB6IE0gNiAxMSBDIDYuNTY0MTI5NCAxMSA3IDExLjQzNTg3MSA3IDEyIEMgNyAxMi41NjQxMjkgNi41NjQxMjk0IDEzIDYgMTMgQyA1LjQzNTg3MDYgMTMgNSAxMi41NjQxMjkgNSAxMiBDIDUgMTEuNDM1ODcxIDUuNDM1ODcwNiAxMSA2IDExIHogTSAxOCAxOCBDIDE4LjU2NDEyOSAxOCAxOSAxOC40MzU4NzEgMTkgMTkgQyAxOSAxOS41NjQxMjkgMTguNTY0MTI5IDIwIDE4IDIwIEMgMTcuNDM1ODcxIDIwIDE3IDE5LjU2NDEyOSAxNyAxOSBDIDE3IDE4LjQzNTg3MSAxNy40MzU4NzEgMTggMTggMTggeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-spreadsheet: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1jb250cmFzdDEganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNENBRjUwIiBkPSJNMi4yIDIuMnYxNy42aDE3LjZWMi4ySDIuMnptMTUuNCA3LjdoLTUuNVY0LjRoNS41djUuNXpNOS45IDQuNHY1LjVINC40VjQuNGg1LjV6bS01LjUgNy43aDUuNXY1LjVINC40di01LjV6bTcuNyA1LjV2LTUuNWg1LjV2NS41aC01LjV6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-stop: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTAgMGgyNHYyNEgweiIgZmlsbD0ibm9uZSIvPgogICAgICAgIDxwYXRoIGQ9Ik02IDZoMTJ2MTJINnoiLz4KICAgIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-tab: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTIxIDNIM2MtMS4xIDAtMiAuOS0yIDJ2MTRjMCAxLjEuOSAyIDIgMmgxOGMxLjEgMCAyLS45IDItMlY1YzAtMS4xLS45LTItMi0yem0wIDE2SDNWNWgxMHY0aDh2MTB6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-table-rows: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTAgMGgyNHYyNEgweiIgZmlsbD0ibm9uZSIvPgogICAgICAgIDxwYXRoIGQ9Ik0yMSw4SDNWNGgxOFY4eiBNMjEsMTBIM3Y0aDE4VjEweiBNMjEsMTZIM3Y0aDE4VjE2eiIvPgogICAgPC9nPgo8L3N2Zz4K);
  --jp-icon-tag: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjgiIGhlaWdodD0iMjgiIHZpZXdCb3g9IjAgMCA0MyAyOCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CgkJPHBhdGggZD0iTTI4LjgzMzIgMTIuMzM0TDMyLjk5OTggMTYuNTAwN0wzNy4xNjY1IDEyLjMzNEgyOC44MzMyWiIvPgoJCTxwYXRoIGQ9Ik0xNi4yMDk1IDIxLjYxMDRDMTUuNjg3MyAyMi4xMjk5IDE0Ljg0NDMgMjIuMTI5OSAxNC4zMjQ4IDIxLjYxMDRMNi45ODI5IDE0LjcyNDVDNi41NzI0IDE0LjMzOTQgNi4wODMxMyAxMy42MDk4IDYuMDQ3ODYgMTMuMDQ4MkM1Ljk1MzQ3IDExLjUyODggNi4wMjAwMiA4LjYxOTQ0IDYuMDY2MjEgNy4wNzY5NUM2LjA4MjgxIDYuNTE0NzcgNi41NTU0OCA2LjA0MzQ3IDcuMTE4MDQgNi4wMzA1NUM5LjA4ODYzIDUuOTg0NzMgMTMuMjYzOCA1LjkzNTc5IDEzLjY1MTggNi4zMjQyNUwyMS43MzY5IDEzLjYzOUMyMi4yNTYgMTQuMTU4NSAyMS43ODUxIDE1LjQ3MjQgMjEuMjYyIDE1Ljk5NDZMMTYuMjA5NSAyMS42MTA0Wk05Ljc3NTg1IDguMjY1QzkuMzM1NTEgNy44MjU2NiA4LjYyMzUxIDcuODI1NjYgOC4xODI4IDguMjY1QzcuNzQzNDYgOC43MDU3MSA3Ljc0MzQ2IDkuNDE3MzMgOC4xODI4IDkuODU2NjdDOC42MjM4MiAxMC4yOTY0IDkuMzM1ODIgMTAuMjk2NCA5Ljc3NTg1IDkuODU2NjdDMTAuMjE1NiA5LjQxNzMzIDEwLjIxNTYgOC43MDUzMyA5Ljc3NTg1IDguMjY1WiIvPgoJPC9nPgo8L3N2Zz4K);
  --jp-icon-terminal: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0IiA+CiAgICA8cmVjdCBjbGFzcz0ianAtdGVybWluYWwtaWNvbi1iYWNrZ3JvdW5kLWNvbG9yIGpwLWljb24tc2VsZWN0YWJsZSIgd2lkdGg9IjIwIiBoZWlnaHQ9IjIwIiB0cmFuc2Zvcm09InRyYW5zbGF0ZSgyIDIpIiBmaWxsPSIjMzMzMzMzIi8+CiAgICA8cGF0aCBjbGFzcz0ianAtdGVybWluYWwtaWNvbi1jb2xvciBqcC1pY29uLXNlbGVjdGFibGUtaW52ZXJzZSIgZD0iTTUuMDU2NjQgOC43NjE3MkM1LjA1NjY0IDguNTk3NjYgNS4wMzEyNSA4LjQ1MzEyIDQuOTgwNDcgOC4zMjgxMkM0LjkzMzU5IDguMTk5MjIgNC44NTU0NyA4LjA4MjAzIDQuNzQ2MDkgNy45NzY1NkM0LjY0MDYyIDcuODcxMDkgNC41IDcuNzc1MzkgNC4zMjQyMiA3LjY4OTQ1QzQuMTUyMzQgNy41OTk2MSAzLjk0MzM2IDcuNTExNzIgMy42OTcyNyA3LjQyNTc4QzMuMzAyNzMgNy4yODUxNiAyLjk0MzM2IDcuMTM2NzIgMi42MTkxNCA2Ljk4MDQ3QzIuMjk0OTIgNi44MjQyMiAyLjAxNzU4IDYuNjQyNTggMS43ODcxMSA2LjQzNTU1QzEuNTYwNTUgNi4yMjg1MiAxLjM4NDc3IDUuOTg4MjggMS4yNTk3NyA1LjcxNDg0QzEuMTM0NzcgNS40Mzc1IDEuMDcyMjcgNS4xMDkzOCAxLjA3MjI3IDQuNzMwNDdDMS4wNzIyNyA0LjM5ODQ0IDEuMTI4OTEgNC4wOTU3IDEuMjQyMTkgMy44MjIyN0MxLjM1NTQ3IDMuNTQ0OTIgMS41MTU2MiAzLjMwNDY5IDEuNzIyNjYgMy4xMDE1NkMxLjkyOTY5IDIuODk4NDQgMi4xNzk2OSAyLjczNDM3IDIuNDcyNjYgMi42MDkzOEMyLjc2NTYyIDIuNDg0MzggMy4wOTE4IDIuNDA0MyAzLjQ1MTE3IDIuMzY5MTRWMS4xMDkzOEg0LjM4ODY3VjIuMzgwODZDNC43NDAyMyAyLjQyNzczIDUuMDU2NjQgMi41MjM0NCA1LjMzNzg5IDIuNjY3OTdDNS42MTkxNCAyLjgxMjUgNS44NTc0MiAzLjAwMTk1IDYuMDUyNzMgMy4yMzYzM0M2LjI1MTk1IDMuNDY2OCA2LjQwNDMgMy43NDAyMyA2LjUwOTc3IDQuMDU2NjRDNi42MTkxNCA0LjM2OTE0IDYuNjczODMgNC43MjA3IDYuNjczODMgNS4xMTEzM0g1LjA0NDkyQzUuMDQ0OTIgNC42Mzg2NyA0LjkzNzUgNC4yODEyNSA0LjcyMjY2IDQuMDM5MDZDNC41MDc4MSAzLjc5Mjk3IDQuMjE2OCAzLjY2OTkyIDMuODQ5NjEgMy42Njk5MkMzLjY1MDM5IDMuNjY5OTIgMy40NzY1NiAzLjY5NzI3IDMuMzI4MTIgMy43NTE5NUMzLjE4MzU5IDMuODAyNzMgMy4wNjQ0NSAzLjg3Njk1IDIuOTcwNyAzLjk3NDYxQzIuODc2OTUgNC4wNjgzNiAyLjgwNjY0IDQuMTc5NjkgMi43NTk3NyA0LjMwODU5QzIuNzE2OCA0LjQzNzUgMi42OTUzMSA0LjU3ODEyIDIuNjk1MzEgNC43MzA0N0MyLjY5NTMxIDQuODgyODEgMi43MTY4IDUuMDE5NTMgMi43NTk3NyA1LjE0MDYyQzIuODA2NjQgNS4yNTc4MSAyLjg4MjgxIDUuMzY3MTkgMi45ODgyOCA1LjQ2ODc1QzMuMDk3NjYgNS41NzAzMSAzLjI0MDIzIDUuNjY3OTcgMy40MTYwMiA1Ljc2MTcyQzMuNTkxOCA1Ljg1MTU2IDMuODEwNTUgNS45NDMzNiA0LjA3MjI3IDYuMDM3MTFDNC40NjY4IDYuMTg1NTUgNC44MjQyMiA2LjMzOTg0IDUuMTQ0NTMgNi41QzUuNDY0ODQgNi42NTYyNSA1LjczODI4IDYuODM5ODQgNS45NjQ4NCA3LjA1MDc4QzYuMTk1MzEgNy4yNTc4MSA2LjM3MTA5IDcuNSA2LjQ5MjE5IDcuNzc3MzRDNi42MTcxOSA4LjA1MDc4IDYuNjc5NjkgOC4zNzUgNi42Nzk2OSA4Ljc1QzYuNjc5NjkgOS4wOTM3NSA2LjYyMzA1IDkuNDA0MyA2LjUwOTc3IDkuNjgxNjRDNi4zOTY0OCA5Ljk1NTA4IDYuMjM0MzggMTAuMTkxNCA2LjAyMzQ0IDEwLjM5MDZDNS44MTI1IDEwLjU4OTggNS41NTg1OSAxMC43NSA1LjI2MTcyIDEwLjg3MTFDNC45NjQ4NCAxMC45ODgzIDQuNjMyODEgMTEuMDY0NSA0LjI2NTYyIDExLjA5OTZWMTIuMjQ4SDMuMzMzOThWMTEuMDk5NkMzLjAwMTk1IDExLjA2ODQgMi42Nzk2OSAxMC45OTYxIDIuMzY3MTkgMTAuODgyOEMyLjA1NDY5IDEwLjc2NTYgMS43NzczNCAxMC41OTc3IDEuNTM1MTYgMTAuMzc4OUMxLjI5Njg4IDEwLjE2MDIgMS4xMDU0NyA5Ljg4NDc3IDAuOTYwOTM4IDkuNTUyNzNDMC44MTY0MDYgOS4yMTY4IDAuNzQ0MTQxIDguODE0NDUgMC43NDQxNDEgOC4zNDU3SDIuMzc4OTFDMi4zNzg5MSA4LjYyNjk1IDIuNDE5OTIgOC44NjMyOCAyLjUwMTk1IDkuMDU0NjlDMi41ODM5OCA5LjI0MjE5IDIuNjg5NDUgOS4zOTI1OCAyLjgxODM2IDkuNTA1ODZDMi45NTExNyA5LjYxNTIzIDMuMTAxNTYgOS42OTMzNiAzLjI2OTUzIDkuNzQwMjNDMy40Mzc1IDkuNzg3MTEgMy42MDkzOCA5LjgxMDU1IDMuNzg1MTYgOS44MTA1NUM0LjIwMzEyIDkuODEwNTUgNC41MTk1MyA5LjcxMjg5IDQuNzM0MzggOS41MTc1OEM0Ljk0OTIyIDkuMzIyMjcgNS4wNTY2NCA5LjA3MDMxIDUuMDU2NjQgOC43NjE3MlpNMTMuNDE4IDEyLjI3MTVIOC4wNzQyMlYxMUgxMy40MThWMTIuMjcxNVoiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDMuOTUyNjQgNikiIGZpbGw9IndoaXRlIi8+Cjwvc3ZnPgo=);
  --jp-icon-text-editor: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtdGV4dC1lZGl0b3ItaWNvbi1jb2xvciBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiM2MTYxNjEiIGQ9Ik0xNSAxNUgzdjJoMTJ2LTJ6bTAtOEgzdjJoMTJWN3pNMyAxM2gxOHYtMkgzdjJ6bTAgOGgxOHYtMkgzdjJ6TTMgM3YyaDE4VjNIM3oiLz4KPC9zdmc+Cg==);
  --jp-icon-toc: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyNCIgaGVpZ2h0PSIyNCIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIj4KICAgIDxwYXRoIGQ9Ik03LDVIMjFWN0g3VjVNNywxM1YxMUgyMVYxM0g3TTQsNC41QTEuNSwxLjUgMCAwLDEgNS41LDZBMS41LDEuNSAwIDAsMSA0LDcuNUExLjUsMS41IDAgMCwxIDIuNSw2QTEuNSwxLjUgMCAwLDEgNCw0LjVNNCwxMC41QTEuNSwxLjUgMCAwLDEgNS41LDEyQTEuNSwxLjUgMCAwLDEgNCwxMy41QTEuNSwxLjUgMCAwLDEgMi41LDEyQTEuNSwxLjUgMCAwLDEgNCwxMC41TTcsMTlWMTdIMjFWMTlIN000LDE2LjVBMS41LDEuNSAwIDAsMSA1LjUsMThBMS41LDEuNSAwIDAsMSA0LDE5LjVBMS41LDEuNSAwIDAsMSAyLjUsMThBMS41LDEuNSAwIDAsMSA0LDE2LjVaIiAvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-tree-view: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTAgMGgyNHYyNEgweiIgZmlsbD0ibm9uZSIvPgogICAgICAgIDxwYXRoIGQ9Ik0yMiAxMVYzaC03djNIOVYzSDJ2OGg3VjhoMnYxMGg0djNoN3YtOGgtN3YzaC0yVjhoMnYzeiIvPgogICAgPC9nPgo8L3N2Zz4K);
  --jp-icon-trusted: url(data:image/svg+xml;base64,PHN2ZyBmaWxsPSJub25lIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI1Ij4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiIgc3Ryb2tlPSIjMzMzMzMzIiBzdHJva2Utd2lkdGg9IjIiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDIgMykiIGQ9Ik0xLjg2MDk0IDExLjQ0MDlDMC44MjY0NDggOC43NzAyNyAwLjg2Mzc3OSA2LjA1NzY0IDEuMjQ5MDcgNC4xOTkzMkMyLjQ4MjA2IDMuOTMzNDcgNC4wODA2OCAzLjQwMzQ3IDUuNjAxMDIgMi44NDQ5QzcuMjM1NDkgMi4yNDQ0IDguODU2NjYgMS41ODE1IDkuOTg3NiAxLjA5NTM5QzExLjA1OTcgMS41ODM0MSAxMi42MDk0IDIuMjQ0NCAxNC4yMTggMi44NDMzOUMxNS43NTAzIDMuNDEzOTQgMTcuMzk5NSAzLjk1MjU4IDE4Ljc1MzkgNC4yMTM4NUMxOS4xMzY0IDYuMDcxNzcgMTkuMTcwOSA4Ljc3NzIyIDE4LjEzOSAxMS40NDA5QzE3LjAzMDMgMTQuMzAzMiAxNC42NjY4IDE3LjE4NDQgOS45OTk5OSAxOC45MzU0QzUuMzMzMiAxNy4xODQ0IDIuOTY5NjggMTQuMzAzMiAxLjg2MDk0IDExLjQ0MDlaIi8+CiAgICA8cGF0aCBjbGFzcz0ianAtaWNvbjIiIGZpbGw9IiMzMzMzMzMiIHN0cm9rZT0iIzMzMzMzMyIgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoOCA5Ljg2NzE5KSIgZD0iTTIuODYwMTUgNC44NjUzNUwwLjcyNjU0OSAyLjk5OTU5TDAgMy42MzA0NUwyLjg2MDE1IDYuMTMxNTdMOCAwLjYzMDg3Mkw3LjI3ODU3IDBMMi44NjAxNSA0Ljg2NTM1WiIvPgo8L3N2Zz4K);
  --jp-icon-undo: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEyLjUgOGMtMi42NSAwLTUuMDUuOTktNi45IDIuNkwyIDd2OWg5bC0zLjYyLTMuNjJjMS4zOS0xLjE2IDMuMTYtMS44OCA1LjEyLTEuODggMy41NCAwIDYuNTUgMi4zMSA3LjYgNS41bDIuMzctLjc4QzIxLjA4IDExLjAzIDE3LjE1IDggMTIuNSA4eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-user: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTYiIHZpZXdCb3g9IjAgMCAyNCAyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTE2IDdhNCA0IDAgMTEtOCAwIDQgNCAwIDAxOCAwek0xMiAxNGE3IDcgMCAwMC03IDdoMTRhNyA3IDAgMDAtNy03eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-users: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjQiIGhlaWdodD0iMjQiIHZlcnNpb249IjEuMSIgdmlld0JveD0iMCAwIDM2IDI0IiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciPgogPGcgY2xhc3M9ImpwLWljb24zIiB0cmFuc2Zvcm09Im1hdHJpeCgxLjczMjcgMCAwIDEuNzMyNyAtMy42MjgyIC4wOTk1NzcpIiBmaWxsPSIjNjE2MTYxIj4KICA8cGF0aCB0cmFuc2Zvcm09Im1hdHJpeCgxLjUsMCwwLDEuNSwwLC02KSIgZD0ibTEyLjE4NiA3LjUwOThjLTEuMDUzNSAwLTEuOTc1NyAwLjU2NjUtMi40Nzg1IDEuNDEwMiAwLjc1MDYxIDAuMzEyNzcgMS4zOTc0IDAuODI2NDggMS44NzMgMS40NzI3aDMuNDg2M2MwLTEuNTkyLTEuMjg4OS0yLjg4MjgtMi44ODA5LTIuODgyOHoiLz4KICA8cGF0aCBkPSJtMjAuNDY1IDIuMzg5NWEyLjE4ODUgMi4xODg1IDAgMCAxLTIuMTg4NCAyLjE4ODUgMi4xODg1IDIuMTg4NSAwIDAgMS0yLjE4ODUtMi4xODg1IDIuMTg4NSAyLjE4ODUgMCAwIDEgMi4xODg1LTIuMTg4NSAyLjE4ODUgMi4xODg1IDAgMCAxIDIuMTg4NCAyLjE4ODV6Ii8+CiAgPHBhdGggdHJhbnNmb3JtPSJtYXRyaXgoMS41LDAsMCwxLjUsMCwtNikiIGQ9Im0zLjU4OTggOC40MjE5Yy0xLjExMjYgMC0yLjAxMzcgMC45MDExMS0yLjAxMzcgMi4wMTM3aDIuODE0NWMwLjI2Nzk3LTAuMzczMDkgMC41OTA3LTAuNzA0MzUgMC45NTg5OC0wLjk3ODUyLTAuMzQ0MzMtMC42MTY4OC0xLjAwMzEtMS4wMzUyLTEuNzU5OC0xLjAzNTJ6Ii8+CiAgPHBhdGggZD0ibTYuOTE1NCA0LjYyM2ExLjUyOTQgMS41Mjk0IDAgMCAxLTEuNTI5NCAxLjUyOTQgMS41Mjk0IDEuNTI5NCAwIDAgMS0xLjUyOTQtMS41Mjk0IDEuNTI5NCAxLjUyOTQgMCAwIDEgMS41Mjk0LTEuNTI5NCAxLjUyOTQgMS41Mjk0IDAgMCAxIDEuNTI5NCAxLjUyOTR6Ii8+CiAgPHBhdGggZD0ibTYuMTM1IDEzLjUzNWMwLTMuMjM5MiAyLjYyNTktNS44NjUgNS44NjUtNS44NjUgMy4yMzkyIDAgNS44NjUgMi42MjU5IDUuODY1IDUuODY1eiIvPgogIDxjaXJjbGUgY3g9IjEyIiBjeT0iMy43Njg1IiByPSIyLjk2ODUiLz4KIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-vega: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8ZyBjbGFzcz0ianAtaWNvbjEganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjMjEyMTIxIj4KICAgIDxwYXRoIGQ9Ik0xMC42IDUuNGwyLjItMy4ySDIuMnY3LjNsNC02LjZ6Ii8+CiAgICA8cGF0aCBkPSJNMTUuOCAyLjJsLTQuNCA2LjZMNyA2LjNsLTQuOCA4djUuNWgxNy42VjIuMmgtNHptLTcgMTUuNEg1LjV2LTQuNGgzLjN2NC40em00LjQgMEg5LjhWOS44aDMuNHY3Ljh6bTQuNCAwaC0zLjRWNi41aDMuNHYxMS4xeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-word: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwIDIwIj4KIDxnIGNsYXNzPSJqcC1pY29uMiIgZmlsbD0iIzQxNDE0MSI+CiAgPHJlY3QgeD0iMiIgeT0iMiIgd2lkdGg9IjE2IiBoZWlnaHQ9IjE2Ii8+CiA8L2c+CiA8ZyBjbGFzcz0ianAtaWNvbi1hY2NlbnQyIiB0cmFuc2Zvcm09InRyYW5zbGF0ZSguNDMgLjA0MDEpIiBmaWxsPSIjZmZmIj4KICA8cGF0aCBkPSJtNC4xNCA4Ljc2cTAuMDY4Mi0xLjg5IDIuNDItMS44OSAxLjE2IDAgMS42OCAwLjQyIDAuNTY3IDAuNDEgMC41NjcgMS4xNnYzLjQ3cTAgMC40NjIgMC41MTQgMC40NjIgMC4xMDMgMCAwLjItMC4wMjMxdjAuNzE0cS0wLjM5OSAwLjEwMy0wLjY1MSAwLjEwMy0wLjQ1MiAwLTAuNjkzLTAuMjItMC4yMzEtMC4yLTAuMjg0LTAuNjYyLTAuOTU2IDAuODcyLTIgMC44NzItMC45MDMgMC0xLjQ3LTAuNDcyLTAuNTI1LTAuNDcyLTAuNTI1LTEuMjYgMC0wLjI2MiAwLjA0NTItMC40NzIgMC4wNTY3LTAuMjIgMC4xMTYtMC4zNzggMC4wNjgyLTAuMTY4IDAuMjMxLTAuMzA0IDAuMTU4LTAuMTQ3IDAuMjYyLTAuMjQyIDAuMTE2LTAuMDkxNCAwLjM2OC0wLjE2OCAwLjI2Mi0wLjA5MTQgMC4zOTktMC4xMjYgMC4xMzYtMC4wNDUyIDAuNDcyLTAuMTAzIDAuMzM2LTAuMDU3OCAwLjUwNC0wLjA3OTggMC4xNTgtMC4wMjMxIDAuNTY3LTAuMDc5OCAwLjU1Ni0wLjA2ODIgMC43NzctMC4yMjEgMC4yMi0wLjE1MiAwLjIyLTAuNDQxdi0wLjI1MnEwLTAuNDMtMC4zNTctMC42NjItMC4zMzYtMC4yMzEtMC45NzYtMC4yMzEtMC42NjIgMC0wLjk5OCAwLjI2Mi0wLjMzNiAwLjI1Mi0wLjM5OSAwLjc5OHptMS44OSAzLjY4cTAuNzg4IDAgMS4yNi0wLjQxIDAuNTA0LTAuNDIgMC41MDQtMC45MDN2LTEuMDVxLTAuMjg0IDAuMTM2LTAuODYxIDAuMjMxLTAuNTY3IDAuMDkxNC0wLjk4NyAwLjE1OC0wLjQyIDAuMDY4Mi0wLjc2NiAwLjMyNi0wLjMzNiAwLjI1Mi0wLjMzNiAwLjcwNHQwLjMwNCAwLjcwNCAwLjg2MSAwLjI1MnoiIHN0cm9rZS13aWR0aD0iMS4wNSIvPgogIDxwYXRoIGQ9Im0xMCA0LjU2aDAuOTQ1djMuMTVxMC42NTEtMC45NzYgMS44OS0wLjk3NiAxLjE2IDAgMS44OSAwLjg0IDAuNjgyIDAuODQgMC42ODIgMi4zMSAwIDEuNDctMC43MDQgMi40Mi0wLjcwNCAwLjg4Mi0xLjg5IDAuODgyLTEuMjYgMC0xLjg5LTEuMDJ2MC43NjZoLTAuODV6bTIuNjIgMy4wNHEtMC43NDYgMC0xLjE2IDAuNjQtMC40NTIgMC42My0wLjQ1MiAxLjY4IDAgMS4wNSAwLjQ1MiAxLjY4dDEuMTYgMC42M3EwLjc3NyAwIDEuMjYtMC42MyAwLjQ5NC0wLjY0IDAuNDk0LTEuNjggMC0xLjA1LTAuNDcyLTEuNjgtMC40NjItMC42NC0xLjI2LTAuNjR6IiBzdHJva2Utd2lkdGg9IjEuMDUiLz4KICA8cGF0aCBkPSJtMi43MyAxNS44IDEzLjYgMC4wMDgxYzAuMDA2OSAwIDAtMi42IDAtMi42IDAtMC4wMDc4LTEuMTUgMC0xLjE1IDAtMC4wMDY5IDAtMC4wMDgzIDEuNS0wLjAwODMgMS41LTJlLTMgLTAuMDAxNC0xMS4zLTAuMDAxNC0xMS4zLTAuMDAxNGwtMC4wMDU5Mi0xLjVjMC0wLjAwNzgtMS4xNyAwLjAwMTMtMS4xNyAwLjAwMTN6IiBzdHJva2Utd2lkdGg9Ii45NzUiLz4KIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-yaml: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8ZyBjbGFzcz0ianAtaWNvbi1jb250cmFzdDIganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjRDgxQjYwIj4KICAgIDxwYXRoIGQ9Ik03LjIgMTguNnYtNS40TDMgNS42aDMuM2wxLjQgMy4xYy4zLjkuNiAxLjYgMSAyLjUuMy0uOC42LTEuNiAxLTIuNWwxLjQtMy4xaDMuNGwtNC40IDcuNnY1LjVsLTIuOS0uMXoiLz4KICAgIDxjaXJjbGUgY2xhc3M9InN0MCIgY3g9IjE3LjYiIGN5PSIxNi41IiByPSIyLjEiLz4KICAgIDxjaXJjbGUgY2xhc3M9InN0MCIgY3g9IjE3LjYiIGN5PSIxMSIgcj0iMi4xIi8+CiAgPC9nPgo8L3N2Zz4K);
}

/* Icon CSS class declarations */

.jp-AddAboveIcon {
  background-image: var(--jp-icon-add-above);
}

.jp-AddBelowIcon {
  background-image: var(--jp-icon-add-below);
}

.jp-AddIcon {
  background-image: var(--jp-icon-add);
}

.jp-BellIcon {
  background-image: var(--jp-icon-bell);
}

.jp-BugDotIcon {
  background-image: var(--jp-icon-bug-dot);
}

.jp-BugIcon {
  background-image: var(--jp-icon-bug);
}

.jp-BuildIcon {
  background-image: var(--jp-icon-build);
}

.jp-CaretDownEmptyIcon {
  background-image: var(--jp-icon-caret-down-empty);
}

.jp-CaretDownEmptyThinIcon {
  background-image: var(--jp-icon-caret-down-empty-thin);
}

.jp-CaretDownIcon {
  background-image: var(--jp-icon-caret-down);
}

.jp-CaretLeftIcon {
  background-image: var(--jp-icon-caret-left);
}

.jp-CaretRightIcon {
  background-image: var(--jp-icon-caret-right);
}

.jp-CaretUpEmptyThinIcon {
  background-image: var(--jp-icon-caret-up-empty-thin);
}

.jp-CaretUpIcon {
  background-image: var(--jp-icon-caret-up);
}

.jp-CaseSensitiveIcon {
  background-image: var(--jp-icon-case-sensitive);
}

.jp-CheckIcon {
  background-image: var(--jp-icon-check);
}

.jp-CircleEmptyIcon {
  background-image: var(--jp-icon-circle-empty);
}

.jp-CircleIcon {
  background-image: var(--jp-icon-circle);
}

.jp-ClearIcon {
  background-image: var(--jp-icon-clear);
}

.jp-CloseIcon {
  background-image: var(--jp-icon-close);
}

.jp-CodeCheckIcon {
  background-image: var(--jp-icon-code-check);
}

.jp-CodeIcon {
  background-image: var(--jp-icon-code);
}

.jp-CollapseAllIcon {
  background-image: var(--jp-icon-collapse-all);
}

.jp-ConsoleIcon {
  background-image: var(--jp-icon-console);
}

.jp-CopyIcon {
  background-image: var(--jp-icon-copy);
}

.jp-CopyrightIcon {
  background-image: var(--jp-icon-copyright);
}

.jp-CutIcon {
  background-image: var(--jp-icon-cut);
}

.jp-DeleteIcon {
  background-image: var(--jp-icon-delete);
}

.jp-DownloadIcon {
  background-image: var(--jp-icon-download);
}

.jp-DuplicateIcon {
  background-image: var(--jp-icon-duplicate);
}

.jp-EditIcon {
  background-image: var(--jp-icon-edit);
}

.jp-EllipsesIcon {
  background-image: var(--jp-icon-ellipses);
}

.jp-ErrorIcon {
  background-image: var(--jp-icon-error);
}

.jp-ExpandAllIcon {
  background-image: var(--jp-icon-expand-all);
}

.jp-ExtensionIcon {
  background-image: var(--jp-icon-extension);
}

.jp-FastForwardIcon {
  background-image: var(--jp-icon-fast-forward);
}

.jp-FileIcon {
  background-image: var(--jp-icon-file);
}

.jp-FileUploadIcon {
  background-image: var(--jp-icon-file-upload);
}

.jp-FilterDotIcon {
  background-image: var(--jp-icon-filter-dot);
}

.jp-FilterIcon {
  background-image: var(--jp-icon-filter);
}

.jp-FilterListIcon {
  background-image: var(--jp-icon-filter-list);
}

.jp-FolderFavoriteIcon {
  background-image: var(--jp-icon-folder-favorite);
}

.jp-FolderIcon {
  background-image: var(--jp-icon-folder);
}

.jp-HomeIcon {
  background-image: var(--jp-icon-home);
}

.jp-Html5Icon {
  background-image: var(--jp-icon-html5);
}

.jp-ImageIcon {
  background-image: var(--jp-icon-image);
}

.jp-InfoIcon {
  background-image: var(--jp-icon-info);
}

.jp-InspectorIcon {
  background-image: var(--jp-icon-inspector);
}

.jp-JsonIcon {
  background-image: var(--jp-icon-json);
}

.jp-JuliaIcon {
  background-image: var(--jp-icon-julia);
}

.jp-JupyterFaviconIcon {
  background-image: var(--jp-icon-jupyter-favicon);
}

.jp-JupyterIcon {
  background-image: var(--jp-icon-jupyter);
}

.jp-JupyterlabWordmarkIcon {
  background-image: var(--jp-icon-jupyterlab-wordmark);
}

.jp-KernelIcon {
  background-image: var(--jp-icon-kernel);
}

.jp-KeyboardIcon {
  background-image: var(--jp-icon-keyboard);
}

.jp-LaunchIcon {
  background-image: var(--jp-icon-launch);
}

.jp-LauncherIcon {
  background-image: var(--jp-icon-launcher);
}

.jp-LineFormIcon {
  background-image: var(--jp-icon-line-form);
}

.jp-LinkIcon {
  background-image: var(--jp-icon-link);
}

.jp-ListIcon {
  background-image: var(--jp-icon-list);
}

.jp-MarkdownIcon {
  background-image: var(--jp-icon-markdown);
}

.jp-MoveDownIcon {
  background-image: var(--jp-icon-move-down);
}

.jp-MoveUpIcon {
  background-image: var(--jp-icon-move-up);
}

.jp-NewFolderIcon {
  background-image: var(--jp-icon-new-folder);
}

.jp-NotTrustedIcon {
  background-image: var(--jp-icon-not-trusted);
}

.jp-NotebookIcon {
  background-image: var(--jp-icon-notebook);
}

.jp-NumberingIcon {
  background-image: var(--jp-icon-numbering);
}

.jp-OfflineBoltIcon {
  background-image: var(--jp-icon-offline-bolt);
}

.jp-PaletteIcon {
  background-image: var(--jp-icon-palette);
}

.jp-PasteIcon {
  background-image: var(--jp-icon-paste);
}

.jp-PdfIcon {
  background-image: var(--jp-icon-pdf);
}

.jp-PythonIcon {
  background-image: var(--jp-icon-python);
}

.jp-RKernelIcon {
  background-image: var(--jp-icon-r-kernel);
}

.jp-ReactIcon {
  background-image: var(--jp-icon-react);
}

.jp-RedoIcon {
  background-image: var(--jp-icon-redo);
}

.jp-RefreshIcon {
  background-image: var(--jp-icon-refresh);
}

.jp-RegexIcon {
  background-image: var(--jp-icon-regex);
}

.jp-RunIcon {
  background-image: var(--jp-icon-run);
}

.jp-RunningIcon {
  background-image: var(--jp-icon-running);
}

.jp-SaveIcon {
  background-image: var(--jp-icon-save);
}

.jp-SearchIcon {
  background-image: var(--jp-icon-search);
}

.jp-SettingsIcon {
  background-image: var(--jp-icon-settings);
}

.jp-ShareIcon {
  background-image: var(--jp-icon-share);
}

.jp-SpreadsheetIcon {
  background-image: var(--jp-icon-spreadsheet);
}

.jp-StopIcon {
  background-image: var(--jp-icon-stop);
}

.jp-TabIcon {
  background-image: var(--jp-icon-tab);
}

.jp-TableRowsIcon {
  background-image: var(--jp-icon-table-rows);
}

.jp-TagIcon {
  background-image: var(--jp-icon-tag);
}

.jp-TerminalIcon {
  background-image: var(--jp-icon-terminal);
}

.jp-TextEditorIcon {
  background-image: var(--jp-icon-text-editor);
}

.jp-TocIcon {
  background-image: var(--jp-icon-toc);
}

.jp-TreeViewIcon {
  background-image: var(--jp-icon-tree-view);
}

.jp-TrustedIcon {
  background-image: var(--jp-icon-trusted);
}

.jp-UndoIcon {
  background-image: var(--jp-icon-undo);
}

.jp-UserIcon {
  background-image: var(--jp-icon-user);
}

.jp-UsersIcon {
  background-image: var(--jp-icon-users);
}

.jp-VegaIcon {
  background-image: var(--jp-icon-vega);
}

.jp-WordIcon {
  background-image: var(--jp-icon-word);
}

.jp-YamlIcon {
  background-image: var(--jp-icon-yaml);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/**
 * (DEPRECATED) Support for consuming icons as CSS background images
 */

.jp-Icon,
.jp-MaterialIcon {
  background-position: center;
  background-repeat: no-repeat;
  background-size: 16px;
  min-width: 16px;
  min-height: 16px;
}

.jp-Icon-cover {
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
}

/**
 * (DEPRECATED) Support for specific CSS icon sizes
 */

.jp-Icon-16 {
  background-size: 16px;
  min-width: 16px;
  min-height: 16px;
}

.jp-Icon-18 {
  background-size: 18px;
  min-width: 18px;
  min-height: 18px;
}

.jp-Icon-20 {
  background-size: 20px;
  min-width: 20px;
  min-height: 20px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.lm-TabBar .lm-TabBar-addButton {
  align-items: center;
  display: flex;
  padding: 4px;
  padding-bottom: 5px;
  margin-right: 1px;
  background-color: var(--jp-layout-color2);
}

.lm-TabBar .lm-TabBar-addButton:hover {
  background-color: var(--jp-layout-color1);
}

.lm-DockPanel-tabBar .lm-TabBar-tab {
  width: var(--jp-private-horizontal-tab-width);
}

.lm-DockPanel-tabBar .lm-TabBar-content {
  flex: unset;
}

.lm-DockPanel-tabBar[data-orientation='horizontal'] {
  flex: 1 1 auto;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/**
 * Support for icons as inline SVG HTMLElements
 */

/* recolor the primary elements of an icon */
.jp-icon0[fill] {
  fill: var(--jp-inverse-layout-color0);
}

.jp-icon1[fill] {
  fill: var(--jp-inverse-layout-color1);
}

.jp-icon2[fill] {
  fill: var(--jp-inverse-layout-color2);
}

.jp-icon3[fill] {
  fill: var(--jp-inverse-layout-color3);
}

.jp-icon4[fill] {
  fill: var(--jp-inverse-layout-color4);
}

.jp-icon0[stroke] {
  stroke: var(--jp-inverse-layout-color0);
}

.jp-icon1[stroke] {
  stroke: var(--jp-inverse-layout-color1);
}

.jp-icon2[stroke] {
  stroke: var(--jp-inverse-layout-color2);
}

.jp-icon3[stroke] {
  stroke: var(--jp-inverse-layout-color3);
}

.jp-icon4[stroke] {
  stroke: var(--jp-inverse-layout-color4);
}

/* recolor the accent elements of an icon */
.jp-icon-accent0[fill] {
  fill: var(--jp-layout-color0);
}

.jp-icon-accent1[fill] {
  fill: var(--jp-layout-color1);
}

.jp-icon-accent2[fill] {
  fill: var(--jp-layout-color2);
}

.jp-icon-accent3[fill] {
  fill: var(--jp-layout-color3);
}

.jp-icon-accent4[fill] {
  fill: var(--jp-layout-color4);
}

.jp-icon-accent0[stroke] {
  stroke: var(--jp-layout-color0);
}

.jp-icon-accent1[stroke] {
  stroke: var(--jp-layout-color1);
}

.jp-icon-accent2[stroke] {
  stroke: var(--jp-layout-color2);
}

.jp-icon-accent3[stroke] {
  stroke: var(--jp-layout-color3);
}

.jp-icon-accent4[stroke] {
  stroke: var(--jp-layout-color4);
}

/* set the color of an icon to transparent */
.jp-icon-none[fill] {
  fill: none;
}

.jp-icon-none[stroke] {
  stroke: none;
}

/* brand icon colors. Same for light and dark */
.jp-icon-brand0[fill] {
  fill: var(--jp-brand-color0);
}

.jp-icon-brand1[fill] {
  fill: var(--jp-brand-color1);
}

.jp-icon-brand2[fill] {
  fill: var(--jp-brand-color2);
}

.jp-icon-brand3[fill] {
  fill: var(--jp-brand-color3);
}

.jp-icon-brand4[fill] {
  fill: var(--jp-brand-color4);
}

.jp-icon-brand0[stroke] {
  stroke: var(--jp-brand-color0);
}

.jp-icon-brand1[stroke] {
  stroke: var(--jp-brand-color1);
}

.jp-icon-brand2[stroke] {
  stroke: var(--jp-brand-color2);
}

.jp-icon-brand3[stroke] {
  stroke: var(--jp-brand-color3);
}

.jp-icon-brand4[stroke] {
  stroke: var(--jp-brand-color4);
}

/* warn icon colors. Same for light and dark */
.jp-icon-warn0[fill] {
  fill: var(--jp-warn-color0);
}

.jp-icon-warn1[fill] {
  fill: var(--jp-warn-color1);
}

.jp-icon-warn2[fill] {
  fill: var(--jp-warn-color2);
}

.jp-icon-warn3[fill] {
  fill: var(--jp-warn-color3);
}

.jp-icon-warn0[stroke] {
  stroke: var(--jp-warn-color0);
}

.jp-icon-warn1[stroke] {
  stroke: var(--jp-warn-color1);
}

.jp-icon-warn2[stroke] {
  stroke: var(--jp-warn-color2);
}

.jp-icon-warn3[stroke] {
  stroke: var(--jp-warn-color3);
}

/* icon colors that contrast well with each other and most backgrounds */
.jp-icon-contrast0[fill] {
  fill: var(--jp-icon-contrast-color0);
}

.jp-icon-contrast1[fill] {
  fill: var(--jp-icon-contrast-color1);
}

.jp-icon-contrast2[fill] {
  fill: var(--jp-icon-contrast-color2);
}

.jp-icon-contrast3[fill] {
  fill: var(--jp-icon-contrast-color3);
}

.jp-icon-contrast0[stroke] {
  stroke: var(--jp-icon-contrast-color0);
}

.jp-icon-contrast1[stroke] {
  stroke: var(--jp-icon-contrast-color1);
}

.jp-icon-contrast2[stroke] {
  stroke: var(--jp-icon-contrast-color2);
}

.jp-icon-contrast3[stroke] {
  stroke: var(--jp-icon-contrast-color3);
}

.jp-icon-dot[fill] {
  fill: var(--jp-warn-color0);
}

.jp-jupyter-icon-color[fill] {
  fill: var(--jp-jupyter-icon-color, var(--jp-warn-color0));
}

.jp-notebook-icon-color[fill] {
  fill: var(--jp-notebook-icon-color, var(--jp-warn-color0));
}

.jp-json-icon-color[fill] {
  fill: var(--jp-json-icon-color, var(--jp-warn-color1));
}

.jp-console-icon-color[fill] {
  fill: var(--jp-console-icon-color, white);
}

.jp-console-icon-background-color[fill] {
  fill: var(--jp-console-icon-background-color, var(--jp-brand-color1));
}

.jp-terminal-icon-color[fill] {
  fill: var(--jp-terminal-icon-color, var(--jp-layout-color2));
}

.jp-terminal-icon-background-color[fill] {
  fill: var(
    --jp-terminal-icon-background-color,
    var(--jp-inverse-layout-color2)
  );
}

.jp-text-editor-icon-color[fill] {
  fill: var(--jp-text-editor-icon-color, var(--jp-inverse-layout-color3));
}

.jp-inspector-icon-color[fill] {
  fill: var(--jp-inspector-icon-color, var(--jp-inverse-layout-color3));
}

/* CSS for icons in selected filebrowser listing items */
.jp-DirListing-item.jp-mod-selected .jp-icon-selectable[fill] {
  fill: #fff;
}

.jp-DirListing-item.jp-mod-selected .jp-icon-selectable-inverse[fill] {
  fill: var(--jp-brand-color1);
}

/* stylelint-disable selector-max-class, selector-max-compound-selectors */

/**
* TODO: come up with non css-hack solution for showing the busy icon on top
*  of the close icon
* CSS for complex behavior of close icon of tabs in the main area tabbar
*/
.lm-DockPanel-tabBar
  .lm-TabBar-tab.lm-mod-closable.jp-mod-dirty
  > .lm-TabBar-tabCloseIcon
  > :not(:hover)
  > .jp-icon3[fill] {
  fill: none;
}

.lm-DockPanel-tabBar
  .lm-TabBar-tab.lm-mod-closable.jp-mod-dirty
  > .lm-TabBar-tabCloseIcon
  > :not(:hover)
  > .jp-icon-busy[fill] {
  fill: var(--jp-inverse-layout-color3);
}

/* stylelint-enable selector-max-class, selector-max-compound-selectors */

/* CSS for icons in status bar */
#jp-main-statusbar .jp-mod-selected .jp-icon-selectable[fill] {
  fill: #fff;
}

#jp-main-statusbar .jp-mod-selected .jp-icon-selectable-inverse[fill] {
  fill: var(--jp-brand-color1);
}

/* special handling for splash icon CSS. While the theme CSS reloads during
   splash, the splash icon can loose theming. To prevent that, we set a
   default for its color variable */
:root {
  --jp-warn-color0: var(--md-orange-700);
}

/* not sure what to do with this one, used in filebrowser listing */
.jp-DragIcon {
  margin-right: 4px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/**
 * Support for alt colors for icons as inline SVG HTMLElements
 */

/* alt recolor the primary elements of an icon */
.jp-icon-alt .jp-icon0[fill] {
  fill: var(--jp-layout-color0);
}

.jp-icon-alt .jp-icon1[fill] {
  fill: var(--jp-layout-color1);
}

.jp-icon-alt .jp-icon2[fill] {
  fill: var(--jp-layout-color2);
}

.jp-icon-alt .jp-icon3[fill] {
  fill: var(--jp-layout-color3);
}

.jp-icon-alt .jp-icon4[fill] {
  fill: var(--jp-layout-color4);
}

.jp-icon-alt .jp-icon0[stroke] {
  stroke: var(--jp-layout-color0);
}

.jp-icon-alt .jp-icon1[stroke] {
  stroke: var(--jp-layout-color1);
}

.jp-icon-alt .jp-icon2[stroke] {
  stroke: var(--jp-layout-color2);
}

.jp-icon-alt .jp-icon3[stroke] {
  stroke: var(--jp-layout-color3);
}

.jp-icon-alt .jp-icon4[stroke] {
  stroke: var(--jp-layout-color4);
}

/* alt recolor the accent elements of an icon */
.jp-icon-alt .jp-icon-accent0[fill] {
  fill: var(--jp-inverse-layout-color0);
}

.jp-icon-alt .jp-icon-accent1[fill] {
  fill: var(--jp-inverse-layout-color1);
}

.jp-icon-alt .jp-icon-accent2[fill] {
  fill: var(--jp-inverse-layout-color2);
}

.jp-icon-alt .jp-icon-accent3[fill] {
  fill: var(--jp-inverse-layout-color3);
}

.jp-icon-alt .jp-icon-accent4[fill] {
  fill: var(--jp-inverse-layout-color4);
}

.jp-icon-alt .jp-icon-accent0[stroke] {
  stroke: var(--jp-inverse-layout-color0);
}

.jp-icon-alt .jp-icon-accent1[stroke] {
  stroke: var(--jp-inverse-layout-color1);
}

.jp-icon-alt .jp-icon-accent2[stroke] {
  stroke: var(--jp-inverse-layout-color2);
}

.jp-icon-alt .jp-icon-accent3[stroke] {
  stroke: var(--jp-inverse-layout-color3);
}

.jp-icon-alt .jp-icon-accent4[stroke] {
  stroke: var(--jp-inverse-layout-color4);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-icon-hoverShow:not(:hover) .jp-icon-hoverShow-content {
  display: none !important;
}

/**
 * Support for hover colors for icons as inline SVG HTMLElements
 */

/**
 * regular colors
 */

/* recolor the primary elements of an icon */
.jp-icon-hover :hover .jp-icon0-hover[fill] {
  fill: var(--jp-inverse-layout-color0);
}

.jp-icon-hover :hover .jp-icon1-hover[fill] {
  fill: var(--jp-inverse-layout-color1);
}

.jp-icon-hover :hover .jp-icon2-hover[fill] {
  fill: var(--jp-inverse-layout-color2);
}

.jp-icon-hover :hover .jp-icon3-hover[fill] {
  fill: var(--jp-inverse-layout-color3);
}

.jp-icon-hover :hover .jp-icon4-hover[fill] {
  fill: var(--jp-inverse-layout-color4);
}

.jp-icon-hover :hover .jp-icon0-hover[stroke] {
  stroke: var(--jp-inverse-layout-color0);
}

.jp-icon-hover :hover .jp-icon1-hover[stroke] {
  stroke: var(--jp-inverse-layout-color1);
}

.jp-icon-hover :hover .jp-icon2-hover[stroke] {
  stroke: var(--jp-inverse-layout-color2);
}

.jp-icon-hover :hover .jp-icon3-hover[stroke] {
  stroke: var(--jp-inverse-layout-color3);
}

.jp-icon-hover :hover .jp-icon4-hover[stroke] {
  stroke: var(--jp-inverse-layout-color4);
}

/* recolor the accent elements of an icon */
.jp-icon-hover :hover .jp-icon-accent0-hover[fill] {
  fill: var(--jp-layout-color0);
}

.jp-icon-hover :hover .jp-icon-accent1-hover[fill] {
  fill: var(--jp-layout-color1);
}

.jp-icon-hover :hover .jp-icon-accent2-hover[fill] {
  fill: var(--jp-layout-color2);
}

.jp-icon-hover :hover .jp-icon-accent3-hover[fill] {
  fill: var(--jp-layout-color3);
}

.jp-icon-hover :hover .jp-icon-accent4-hover[fill] {
  fill: var(--jp-layout-color4);
}

.jp-icon-hover :hover .jp-icon-accent0-hover[stroke] {
  stroke: var(--jp-layout-color0);
}

.jp-icon-hover :hover .jp-icon-accent1-hover[stroke] {
  stroke: var(--jp-layout-color1);
}

.jp-icon-hover :hover .jp-icon-accent2-hover[stroke] {
  stroke: var(--jp-layout-color2);
}

.jp-icon-hover :hover .jp-icon-accent3-hover[stroke] {
  stroke: var(--jp-layout-color3);
}

.jp-icon-hover :hover .jp-icon-accent4-hover[stroke] {
  stroke: var(--jp-layout-color4);
}

/* set the color of an icon to transparent */
.jp-icon-hover :hover .jp-icon-none-hover[fill] {
  fill: none;
}

.jp-icon-hover :hover .jp-icon-none-hover[stroke] {
  stroke: none;
}

/**
 * inverse colors
 */

/* inverse recolor the primary elements of an icon */
.jp-icon-hover.jp-icon-alt :hover .jp-icon0-hover[fill] {
  fill: var(--jp-layout-color0);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon1-hover[fill] {
  fill: var(--jp-layout-color1);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon2-hover[fill] {
  fill: var(--jp-layout-color2);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon3-hover[fill] {
  fill: var(--jp-layout-color3);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon4-hover[fill] {
  fill: var(--jp-layout-color4);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon0-hover[stroke] {
  stroke: var(--jp-layout-color0);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon1-hover[stroke] {
  stroke: var(--jp-layout-color1);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon2-hover[stroke] {
  stroke: var(--jp-layout-color2);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon3-hover[stroke] {
  stroke: var(--jp-layout-color3);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon4-hover[stroke] {
  stroke: var(--jp-layout-color4);
}

/* inverse recolor the accent elements of an icon */
.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent0-hover[fill] {
  fill: var(--jp-inverse-layout-color0);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent1-hover[fill] {
  fill: var(--jp-inverse-layout-color1);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent2-hover[fill] {
  fill: var(--jp-inverse-layout-color2);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent3-hover[fill] {
  fill: var(--jp-inverse-layout-color3);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent4-hover[fill] {
  fill: var(--jp-inverse-layout-color4);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent0-hover[stroke] {
  stroke: var(--jp-inverse-layout-color0);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent1-hover[stroke] {
  stroke: var(--jp-inverse-layout-color1);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent2-hover[stroke] {
  stroke: var(--jp-inverse-layout-color2);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent3-hover[stroke] {
  stroke: var(--jp-inverse-layout-color3);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent4-hover[stroke] {
  stroke: var(--jp-inverse-layout-color4);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-IFrame {
  width: 100%;
  height: 100%;
}

.jp-IFrame > iframe {
  border: none;
}

/*
When drag events occur, `lm-mod-override-cursor` is added to the body.
Because iframes steal all cursor events, the following two rules are necessary
to suppress pointer events while resize drags are occurring. There may be a
better solution to this problem.
*/
body.lm-mod-override-cursor .jp-IFrame {
  position: relative;
}

body.lm-mod-override-cursor .jp-IFrame::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: transparent;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2016, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-HoverBox {
  position: fixed;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-FormGroup-content fieldset {
  border: none;
  padding: 0;
  min-width: 0;
  width: 100%;
}

/* stylelint-disable selector-max-type */

.jp-FormGroup-content fieldset .jp-inputFieldWrapper input,
.jp-FormGroup-content fieldset .jp-inputFieldWrapper select,
.jp-FormGroup-content fieldset .jp-inputFieldWrapper textarea {
  font-size: var(--jp-content-font-size2);
  border-color: var(--jp-input-border-color);
  border-style: solid;
  border-radius: var(--jp-border-radius);
  border-width: 1px;
  padding: 6px 8px;
  background: none;
  color: var(--jp-ui-font-color0);
  height: inherit;
}

.jp-FormGroup-content fieldset input[type='checkbox'] {
  position: relative;
  top: 2px;
  margin-left: 0;
}

.jp-FormGroup-content button.jp-mod-styled {
  cursor: pointer;
}

.jp-FormGroup-content .checkbox label {
  cursor: pointer;
  font-size: var(--jp-content-font-size1);
}

.jp-FormGroup-content .jp-root > fieldset > legend {
  display: none;
}

.jp-FormGroup-content .jp-root > fieldset > p {
  display: none;
}

/** copy of `input.jp-mod-styled:focus` style */
.jp-FormGroup-content fieldset input:focus,
.jp-FormGroup-content fieldset select:focus {
  -moz-outline-radius: unset;
  outline: var(--jp-border-width) solid var(--md-blue-500);
  outline-offset: -1px;
  box-shadow: inset 0 0 4px var(--md-blue-300);
}

.jp-FormGroup-content fieldset input:hover:not(:focus),
.jp-FormGroup-content fieldset select:hover:not(:focus) {
  background-color: var(--jp-border-color2);
}

/* stylelint-enable selector-max-type */

.jp-FormGroup-content .checkbox .field-description {
  /* Disable default description field for checkbox:
   because other widgets do not have description fields,
   we add descriptions to each widget on the field level.
  */
  display: none;
}

.jp-FormGroup-content #root__description {
  display: none;
}

.jp-FormGroup-content .jp-modifiedIndicator {
  width: 5px;
  background-color: var(--jp-brand-color2);
  margin-top: 0;
  margin-left: calc(var(--jp-private-settingeditor-modifier-indent) * -1);
  flex-shrink: 0;
}

.jp-FormGroup-content .jp-modifiedIndicator.jp-errorIndicator {
  background-color: var(--jp-error-color0);
  margin-right: 0.5em;
}

/* RJSF ARRAY style */

.jp-arrayFieldWrapper legend {
  font-size: var(--jp-content-font-size2);
  color: var(--jp-ui-font-color0);
  flex-basis: 100%;
  padding: 4px 0;
  font-weight: var(--jp-content-heading-font-weight);
  border-bottom: 1px solid var(--jp-border-color2);
}

.jp-arrayFieldWrapper .field-description {
  padding: 4px 0;
  white-space: pre-wrap;
}

.jp-arrayFieldWrapper .array-item {
  width: 100%;
  border: 1px solid var(--jp-border-color2);
  border-radius: 4px;
  margin: 4px;
}

.jp-ArrayOperations {
  display: flex;
  margin-left: 8px;
}

.jp-ArrayOperationsButton {
  margin: 2px;
}

.jp-ArrayOperationsButton .jp-icon3[fill] {
  fill: var(--jp-ui-font-color0);
}

button.jp-ArrayOperationsButton.jp-mod-styled:disabled {
  cursor: not-allowed;
  opacity: 0.5;
}

/* RJSF form validation error */

.jp-FormGroup-content .validationErrors {
  color: var(--jp-error-color0);
}

/* Hide panel level error as duplicated the field level error */
.jp-FormGroup-content .panel.errors {
  display: none;
}

/* RJSF normal content (settings-editor) */

.jp-FormGroup-contentNormal {
  display: flex;
  align-items: center;
  flex-wrap: wrap;
}

.jp-FormGroup-contentNormal .jp-FormGroup-contentItem {
  margin-left: 7px;
  color: var(--jp-ui-font-color0);
}

.jp-FormGroup-contentNormal .jp-FormGroup-description {
  flex-basis: 100%;
  padding: 4px 7px;
}

.jp-FormGroup-contentNormal .jp-FormGroup-default {
  flex-basis: 100%;
  padding: 4px 7px;
}

.jp-FormGroup-contentNormal .jp-FormGroup-fieldLabel {
  font-size: var(--jp-content-font-size1);
  font-weight: normal;
  min-width: 120px;
}

.jp-FormGroup-contentNormal fieldset:not(:first-child) {
  margin-left: 7px;
}

.jp-FormGroup-contentNormal .field-array-of-string .array-item {
  /* Display `jp-ArrayOperations` buttons side-by-side with content except
    for small screens where flex-wrap will place them one below the other.
  */
  display: flex;
  align-items: center;
  flex-wrap: wrap;
}

.jp-FormGroup-contentNormal .jp-objectFieldWrapper .form-group {
  padding: 2px 8px 2px var(--jp-private-settingeditor-modifier-indent);
  margin-top: 2px;
}

/* RJSF compact content (metadata-form) */

.jp-FormGroup-content.jp-FormGroup-contentCompact {
  width: 100%;
}

.jp-FormGroup-contentCompact .form-group {
  display: flex;
  padding: 0.5em 0.2em 0.5em 0;
}

.jp-FormGroup-contentCompact
  .jp-FormGroup-compactTitle
  .jp-FormGroup-description {
  font-size: var(--jp-ui-font-size1);
  color: var(--jp-ui-font-color2);
}

.jp-FormGroup-contentCompact .jp-FormGroup-fieldLabel {
  padding-bottom: 0.3em;
}

.jp-FormGroup-contentCompact .jp-inputFieldWrapper .form-control {
  width: 100%;
  box-sizing: border-box;
}

.jp-FormGroup-contentCompact .jp-arrayFieldWrapper .jp-FormGroup-compactTitle {
  padding-bottom: 7px;
}

.jp-FormGroup-contentCompact
  .jp-objectFieldWrapper
  .jp-objectFieldWrapper
  .form-group {
  padding: 2px 8px 2px var(--jp-private-settingeditor-modifier-indent);
  margin-top: 2px;
}

.jp-FormGroup-contentCompact ul.error-detail {
  margin-block-start: 0.5em;
  margin-block-end: 0.5em;
  padding-inline-start: 1em;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

.jp-SidePanel {
  display: flex;
  flex-direction: column;
  min-width: var(--jp-sidebar-min-width);
  overflow-y: auto;
  color: var(--jp-ui-font-color1);
  background: var(--jp-layout-color1);
  font-size: var(--jp-ui-font-size1);
}

.jp-SidePanel-header {
  flex: 0 0 auto;
  display: flex;
  border-bottom: var(--jp-border-width) solid var(--jp-border-color2);
  font-size: var(--jp-ui-font-size0);
  font-weight: 600;
  letter-spacing: 1px;
  margin: 0;
  padding: 2px;
  text-transform: uppercase;
}

.jp-SidePanel-toolbar {
  flex: 0 0 auto;
}

.jp-SidePanel-content {
  flex: 1 1 auto;
}

.jp-SidePanel-toolbar,
.jp-AccordionPanel-toolbar {
  height: var(--jp-private-toolbar-height);
}

.jp-SidePanel-toolbar.jp-Toolbar-micro {
  display: none;
}

.lm-AccordionPanel .jp-AccordionPanel-title {
  box-sizing: border-box;
  line-height: 25px;
  margin: 0;
  display: flex;
  align-items: center;
  background: var(--jp-layout-color1);
  color: var(--jp-ui-font-color1);
  border-bottom: var(--jp-border-width) solid var(--jp-toolbar-border-color);
  box-shadow: var(--jp-toolbar-box-shadow);
  font-size: var(--jp-ui-font-size0);
}

.jp-AccordionPanel-title {
  cursor: pointer;
  user-select: none;
  -moz-user-select: none;
  -webkit-user-select: none;
  text-transform: uppercase;
}

.lm-AccordionPanel[data-orientation='horizontal'] > .jp-AccordionPanel-title {
  /* Title is rotated for horizontal accordion panel using CSS */
  display: block;
  transform-origin: top left;
  transform: rotate(-90deg) translate(-100%);
}

.jp-AccordionPanel-title .lm-AccordionPanel-titleLabel {
  user-select: none;
  text-overflow: ellipsis;
  white-space: nowrap;
  overflow: hidden;
}

.jp-AccordionPanel-title .lm-AccordionPanel-titleCollapser {
  transform: rotate(-90deg);
  margin: auto 0;
  height: 16px;
}

.jp-AccordionPanel-title.lm-mod-expanded .lm-AccordionPanel-titleCollapser {
  transform: rotate(0deg);
}

.lm-AccordionPanel .jp-AccordionPanel-toolbar {
  background: none;
  box-shadow: none;
  border: none;
  margin-left: auto;
}

.lm-AccordionPanel .lm-SplitPanel-handle:hover {
  background: var(--jp-layout-color3);
}

.jp-text-truncated {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2017, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-Spinner {
  position: absolute;
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 10;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background: var(--jp-layout-color0);
  outline: none;
}

.jp-SpinnerContent {
  font-size: 10px;
  margin: 50px auto;
  text-indent: -9999em;
  width: 3em;
  height: 3em;
  border-radius: 50%;
  background: var(--jp-brand-color3);
  background: linear-gradient(
    to right,
    #f37626 10%,
    rgba(255, 255, 255, 0) 42%
  );
  position: relative;
  animation: load3 1s infinite linear, fadeIn 1s;
}

.jp-SpinnerContent::before {
  width: 50%;
  height: 50%;
  background: #f37626;
  border-radius: 100% 0 0;
  position: absolute;
  top: 0;
  left: 0;
  content: '';
}

.jp-SpinnerContent::after {
  background: var(--jp-layout-color0);
  width: 75%;
  height: 75%;
  border-radius: 50%;
  content: '';
  margin: auto;
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
}

@keyframes fadeIn {
  0% {
    opacity: 0;
  }

  100% {
    opacity: 1;
  }
}

@keyframes load3 {
  0% {
    transform: rotate(0deg);
  }

  100% {
    transform: rotate(360deg);
  }
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

button.jp-mod-styled {
  font-size: var(--jp-ui-font-size1);
  color: var(--jp-ui-font-color0);
  border: none;
  box-sizing: border-box;
  text-align: center;
  line-height: 32px;
  height: 32px;
  padding: 0 12px;
  letter-spacing: 0.8px;
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
}

input.jp-mod-styled {
  background: var(--jp-input-background);
  height: 28px;
  box-sizing: border-box;
  border: var(--jp-border-width) solid var(--jp-border-color1);
  padding-left: 7px;
  padding-right: 7px;
  font-size: var(--jp-ui-font-size2);
  color: var(--jp-ui-font-color0);
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
}

input[type='checkbox'].jp-mod-styled {
  appearance: checkbox;
  -webkit-appearance: checkbox;
  -moz-appearance: checkbox;
  height: auto;
}

input.jp-mod-styled:focus {
  border: var(--jp-border-width) solid var(--md-blue-500);
  box-shadow: inset 0 0 4px var(--md-blue-300);
}

.jp-select-wrapper {
  display: flex;
  position: relative;
  flex-direction: column;
  padding: 1px;
  background-color: var(--jp-layout-color1);
  box-sizing: border-box;
  margin-bottom: 12px;
}

.jp-select-wrapper:not(.multiple) {
  height: 28px;
}

.jp-select-wrapper.jp-mod-focused select.jp-mod-styled {
  border: var(--jp-border-width) solid var(--jp-input-active-border-color);
  box-shadow: var(--jp-input-box-shadow);
  background-color: var(--jp-input-active-background);
}

select.jp-mod-styled:hover {
  cursor: pointer;
  color: var(--jp-ui-font-color0);
  background-color: var(--jp-input-hover-background);
  box-shadow: inset 0 0 1px rgba(0, 0, 0, 0.5);
}

select.jp-mod-styled {
  flex: 1 1 auto;
  width: 100%;
  font-size: var(--jp-ui-font-size2);
  background: var(--jp-input-background);
  color: var(--jp-ui-font-color0);
  padding: 0 25px 0 8px;
  border: var(--jp-border-width) solid var(--jp-input-border-color);
  border-radius: 0;
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
}

select.jp-mod-styled:not([multiple]) {
  height: 32px;
}

select.jp-mod-styled[multiple] {
  max-height: 200px;
  overflow-y: auto;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-switch {
  display: flex;
  align-items: center;
  padding-left: 4px;
  padding-right: 4px;
  font-size: var(--jp-ui-font-size1);
  background-color: transparent;
  color: var(--jp-ui-font-color1);
  border: none;
  height: 20px;
}

.jp-switch:hover {
  background-color: var(--jp-layout-color2);
}

.jp-switch-label {
  margin-right: 5px;
  font-family: var(--jp-ui-font-family);
}

.jp-switch-track {
  cursor: pointer;
  background-color: var(--jp-switch-color, var(--jp-border-color1));
  -webkit-transition: 0.4s;
  transition: 0.4s;
  border-radius: 34px;
  height: 16px;
  width: 35px;
  position: relative;
}

.jp-switch-track::before {
  content: '';
  position: absolute;
  height: 10px;
  width: 10px;
  margin: 3px;
  left: 0;
  background-color: var(--jp-ui-inverse-font-color1);
  -webkit-transition: 0.4s;
  transition: 0.4s;
  border-radius: 50%;
}

.jp-switch[aria-checked='true'] .jp-switch-track {
  background-color: var(--jp-switch-true-position-color, var(--jp-warn-color0));
}

.jp-switch[aria-checked='true'] .jp-switch-track::before {
  /* track width (35) - margins (3 + 3) - thumb width (10) */
  left: 19px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2016, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

:root {
  --jp-private-toolbar-height: calc(
    28px + var(--jp-border-width)
  ); /* leave 28px for content */
}

.jp-Toolbar {
  color: var(--jp-ui-font-color1);
  flex: 0 0 auto;
  display: flex;
  flex-direction: row;
  border-bottom: var(--jp-border-width) solid var(--jp-toolbar-border-color);
  box-shadow: var(--jp-toolbar-box-shadow);
  background: var(--jp-toolbar-background);
  min-height: var(--jp-toolbar-micro-height);
  padding: 2px;
  z-index: 8;
  overflow-x: hidden;
}

/* Toolbar items */

.jp-Toolbar > .jp-Toolbar-item.jp-Toolbar-spacer {
  flex-grow: 1;
  flex-shrink: 1;
}

.jp-Toolbar-item.jp-Toolbar-kernelStatus {
  display: inline-block;
  width: 32px;
  background-repeat: no-repeat;
  background-position: center;
  background-size: 16px;
}

.jp-Toolbar > .jp-Toolbar-item {
  flex: 0 0 auto;
  display: flex;
  padding-left: 1px;
  padding-right: 1px;
  font-size: var(--jp-ui-font-size1);
  line-height: var(--jp-private-toolbar-height);
  height: 100%;
}

/* Toolbar buttons */

/* This is the div we use to wrap the react component into a Widget */
div.jp-ToolbarButton {
  color: transparent;
  border: none;
  box-sizing: border-box;
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
  padding: 0;
  margin: 0;
}

button.jp-ToolbarButtonComponent {
  background: var(--jp-layout-color1);
  border: none;
  box-sizing: border-box;
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
  padding: 0 6px;
  margin: 0;
  height: 24px;
  border-radius: var(--jp-border-radius);
  display: flex;
  align-items: center;
  text-align: center;
  font-size: 14px;
  min-width: unset;
  min-height: unset;
}

button.jp-ToolbarButtonComponent:disabled {
  opacity: 0.4;
}

button.jp-ToolbarButtonComponent > span {
  padding: 0;
  flex: 0 0 auto;
}

button.jp-ToolbarButtonComponent .jp-ToolbarButtonComponent-label {
  font-size: var(--jp-ui-font-size1);
  line-height: 100%;
  padding-left: 2px;
  color: var(--jp-ui-font-color1);
  font-family: var(--jp-ui-font-family);
}

#jp-main-dock-panel[data-mode='single-document']
  .jp-MainAreaWidget
  > .jp-Toolbar.jp-Toolbar-micro {
  padding: 0;
  min-height: 0;
}

#jp-main-dock-panel[data-mode='single-document']
  .jp-MainAreaWidget
  > .jp-Toolbar {
  border: none;
  box-shadow: none;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

.jp-WindowedPanel-outer {
  position: relative;
  overflow-y: auto;
}

.jp-WindowedPanel-inner {
  position: relative;
}

.jp-WindowedPanel-window {
  position: absolute;
  left: 0;
  right: 0;
  overflow: visible;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/* Sibling imports */

body {
  color: var(--jp-ui-font-color1);
  font-size: var(--jp-ui-font-size1);
}

/* Disable native link decoration styles everywhere outside of dialog boxes */
a {
  text-decoration: unset;
  color: unset;
}

a:hover {
  text-decoration: unset;
  color: unset;
}

/* Accessibility for links inside dialog box text */
.jp-Dialog-content a {
  text-decoration: revert;
  color: var(--jp-content-link-color);
}

.jp-Dialog-content a:hover {
  text-decoration: revert;
}

/* Styles for ui-components */
.jp-Button {
  color: var(--jp-ui-font-color2);
  border-radius: var(--jp-border-radius);
  padding: 0 12px;
  font-size: var(--jp-ui-font-size1);

  /* Copy from blueprint 3 */
  display: inline-flex;
  flex-direction: row;
  border: none;
  cursor: pointer;
  align-items: center;
  justify-content: center;
  text-align: left;
  vertical-align: middle;
  min-height: 30px;
  min-width: 30px;
}

.jp-Button:disabled {
  cursor: not-allowed;
}

.jp-Button:empty {
  padding: 0 !important;
}

.jp-Button.jp-mod-small {
  min-height: 24px;
  min-width: 24px;
  font-size: 12px;
  padding: 0 7px;
}

/* Use our own theme for hover styles */
.jp-Button.jp-mod-minimal:hover {
  background-color: var(--jp-layout-color2);
}

.jp-Button.jp-mod-minimal {
  background: none;
}

.jp-InputGroup {
  display: block;
  position: relative;
}

.jp-InputGroup input {
  box-sizing: border-box;
  border: none;
  border-radius: 0;
  background-color: transparent;
  color: var(--jp-ui-font-color0);
  box-shadow: inset 0 0 0 var(--jp-border-width) var(--jp-input-border-color);
  padding-bottom: 0;
  padding-top: 0;
  padding-left: 10px;
  padding-right: 28px;
  position: relative;
  width: 100%;
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  font-size: 14px;
  font-weight: 400;
  height: 30px;
  line-height: 30px;
  outline: none;
  vertical-align: middle;
}

.jp-InputGroup input:focus {
  box-shadow: inset 0 0 0 var(--jp-border-width)
      var(--jp-input-active-box-shadow-color),
    inset 0 0 0 3px var(--jp-input-active-box-shadow-color);
}

.jp-InputGroup input:disabled {
  cursor: not-allowed;
  resize: block;
  background-color: var(--jp-layout-color2);
  color: var(--jp-ui-font-color2);
}

.jp-InputGroup input:disabled ~ span {
  cursor: not-allowed;
  color: var(--jp-ui-font-color2);
}

.jp-InputGroup input::placeholder,
input::placeholder {
  color: var(--jp-ui-font-color2);
}

.jp-InputGroupAction {
  position: absolute;
  bottom: 1px;
  right: 0;
  padding: 6px;
}

.jp-HTMLSelect.jp-DefaultStyle select {
  background-color: initial;
  border: none;
  border-radius: 0;
  box-shadow: none;
  color: var(--jp-ui-font-color0);
  display: block;
  font-size: var(--jp-ui-font-size1);
  font-family: var(--jp-ui-font-family);
  height: 24px;
  line-height: 14px;
  padding: 0 25px 0 10px;
  text-align: left;
  -moz-appearance: none;
  -webkit-appearance: none;
}

.jp-HTMLSelect.jp-DefaultStyle select:disabled {
  background-color: var(--jp-layout-color2);
  color: var(--jp-ui-font-color2);
  cursor: not-allowed;
  resize: block;
}

.jp-HTMLSelect.jp-DefaultStyle select:disabled ~ span {
  cursor: not-allowed;
}

/* Use our own theme for hover and option styles */
/* stylelint-disable-next-line selector-max-type */
.jp-HTMLSelect.jp-DefaultStyle select:hover,
.jp-HTMLSelect.jp-DefaultStyle select > option {
  background-color: var(--jp-layout-color2);
  color: var(--jp-ui-font-color0);
}

select {
  box-sizing: border-box;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Styles
|----------------------------------------------------------------------------*/

.jp-StatusBar-Widget {
  display: flex;
  align-items: center;
  background: var(--jp-layout-color2);
  min-height: var(--jp-statusbar-height);
  justify-content: space-between;
  padding: 0 10px;
}

.jp-StatusBar-Left {
  display: flex;
  align-items: center;
  flex-direction: row;
}

.jp-StatusBar-Middle {
  display: flex;
  align-items: center;
}

.jp-StatusBar-Right {
  display: flex;
  align-items: center;
  flex-direction: row-reverse;
}

.jp-StatusBar-Item {
  max-height: var(--jp-statusbar-height);
  margin: 0 2px;
  height: var(--jp-statusbar-height);
  white-space: nowrap;
  text-overflow: ellipsis;
  color: var(--jp-ui-font-color1);
  padding: 0 6px;
}

.jp-mod-highlighted:hover {
  background-color: var(--jp-layout-color3);
}

.jp-mod-clicked {
  background-color: var(--jp-brand-color1);
}

.jp-mod-clicked:hover {
  background-color: var(--jp-brand-color0);
}

.jp-mod-clicked .jp-StatusBar-TextItem {
  color: var(--jp-ui-inverse-font-color1);
}

.jp-StatusBar-HoverItem {
  box-shadow: '0px 4px 4px rgba(0, 0, 0, 0.25)';
}

.jp-StatusBar-TextItem {
  font-size: var(--jp-ui-font-size1);
  font-family: var(--jp-ui-font-family);
  line-height: 24px;
  color: var(--jp-ui-font-color1);
}

.jp-StatusBar-GroupItem {
  display: flex;
  align-items: center;
  flex-direction: row;
}

.jp-Statusbar-ProgressCircle svg {
  display: block;
  margin: 0 auto;
  width: 16px;
  height: 24px;
  align-self: normal;
}

.jp-Statusbar-ProgressCircle path {
  fill: var(--jp-inverse-layout-color3);
}

.jp-Statusbar-ProgressBar-progress-bar {
  height: 10px;
  width: 100px;
  border: solid 0.25px var(--jp-brand-color2);
  border-radius: 3px;
  overflow: hidden;
  align-self: center;
}

.jp-Statusbar-ProgressBar-progress-bar > div {
  background-color: var(--jp-brand-color2);
  background-image: linear-gradient(
    -45deg,
    rgba(255, 255, 255, 0.2) 25%,
    transparent 25%,
    transparent 50%,
    rgba(255, 255, 255, 0.2) 50%,
    rgba(255, 255, 255, 0.2) 75%,
    transparent 75%,
    transparent
  );
  background-size: 40px 40px;
  float: left;
  width: 0%;
  height: 100%;
  font-size: 12px;
  line-height: 14px;
  color: #fff;
  text-align: center;
  animation: jp-Statusbar-ExecutionTime-progress-bar 2s linear infinite;
}

.jp-Statusbar-ProgressBar-progress-bar p {
  color: var(--jp-ui-font-color1);
  font-family: var(--jp-ui-font-family);
  font-size: var(--jp-ui-font-size1);
  line-height: 10px;
  width: 100px;
}

@keyframes jp-Statusbar-ExecutionTime-progress-bar {
  0% {
    background-position: 0 0;
  }

  100% {
    background-position: 40px 40px;
  }
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Variables
|----------------------------------------------------------------------------*/

:root {
  --jp-private-commandpalette-search-height: 28px;
}

/*-----------------------------------------------------------------------------
| Overall styles
|----------------------------------------------------------------------------*/

.lm-CommandPalette {
  padding-bottom: 0;
  color: var(--jp-ui-font-color1);
  background: var(--jp-layout-color1);

  /* This is needed so that all font sizing of children done in ems is
   * relative to this base size */
  font-size: var(--jp-ui-font-size1);
}

/*-----------------------------------------------------------------------------
| Modal variant
|----------------------------------------------------------------------------*/

.jp-ModalCommandPalette {
  position: absolute;
  z-index: 10000;
  top: 38px;
  left: 30%;
  margin: 0;
  padding: 4px;
  width: 40%;
  box-shadow: var(--jp-elevation-z4);
  border-radius: 4px;
  background: var(--jp-layout-color0);
}

.jp-ModalCommandPalette .lm-CommandPalette {
  max-height: 40vh;
}

.jp-ModalCommandPalette .lm-CommandPalette .lm-close-icon::after {
  display: none;
}

.jp-ModalCommandPalette .lm-CommandPalette .lm-CommandPalette-header {
  display: none;
}

.jp-ModalCommandPalette .lm-CommandPalette .lm-CommandPalette-item {
  margin-left: 4px;
  margin-right: 4px;
}

.jp-ModalCommandPalette
  .lm-CommandPalette
  .lm-CommandPalette-item.lm-mod-disabled {
  display: none;
}

/*-----------------------------------------------------------------------------
| Search
|----------------------------------------------------------------------------*/

.lm-CommandPalette-search {
  padding: 4px;
  background-color: var(--jp-layout-color1);
  z-index: 2;
}

.lm-CommandPalette-wrapper {
  overflow: overlay;
  padding: 0 9px;
  background-color: var(--jp-input-active-background);
  height: 30px;
  box-shadow: inset 0 0 0 var(--jp-border-width) var(--jp-input-border-color);
}

.lm-CommandPalette.lm-mod-focused .lm-CommandPalette-wrapper {
  box-shadow: inset 0 0 0 1px var(--jp-input-active-box-shadow-color),
    inset 0 0 0 3px var(--jp-input-active-box-shadow-color);
}

.jp-SearchIconGroup {
  color: white;
  background-color: var(--jp-brand-color1);
  position: absolute;
  top: 4px;
  right: 4px;
  padding: 5px 5px 1px;
}

.jp-SearchIconGroup svg {
  height: 20px;
  width: 20px;
}

.jp-SearchIconGroup .jp-icon3[fill] {
  fill: var(--jp-layout-color0);
}

.lm-CommandPalette-input {
  background: transparent;
  width: calc(100% - 18px);
  float: left;
  border: none;
  outline: none;
  font-size: var(--jp-ui-font-size1);
  color: var(--jp-ui-font-color0);
  line-height: var(--jp-private-commandpalette-search-height);
}

.lm-CommandPalette-input::-webkit-input-placeholder,
.lm-CommandPalette-input::-moz-placeholder,
.lm-CommandPalette-input:-ms-input-placeholder {
  color: var(--jp-ui-font-color2);
  font-size: var(--jp-ui-font-size1);
}

/*-----------------------------------------------------------------------------
| Results
|----------------------------------------------------------------------------*/

.lm-CommandPalette-header:first-child {
  margin-top: 0;
}

.lm-CommandPalette-header {
  border-bottom: solid var(--jp-border-width) var(--jp-border-color2);
  color: var(--jp-ui-font-color1);
  cursor: pointer;
  display: flex;
  font-size: var(--jp-ui-font-size0);
  font-weight: 600;
  letter-spacing: 1px;
  margin-top: 8px;
  padding: 8px 0 8px 12px;
  text-transform: uppercase;
}

.lm-CommandPalette-header.lm-mod-active {
  background: var(--jp-layout-color2);
}

.lm-CommandPalette-header > mark {
  background-color: transparent;
  font-weight: bold;
  color: var(--jp-ui-font-color1);
}

.lm-CommandPalette-item {
  padding: 4px 12px 4px 4px;
  color: var(--jp-ui-font-color1);
  font-size: var(--jp-ui-font-size1);
  font-weight: 400;
  display: flex;
}

.lm-CommandPalette-item.lm-mod-disabled {
  color: var(--jp-ui-font-color2);
}

.lm-CommandPalette-item.lm-mod-active {
  color: var(--jp-ui-inverse-font-color1);
  background: var(--jp-brand-color1);
}

.lm-CommandPalette-item.lm-mod-active .lm-CommandPalette-itemLabel > mark {
  color: var(--jp-ui-inverse-font-color0);
}

.lm-CommandPalette-item.lm-mod-active .jp-icon-selectable[fill] {
  fill: var(--jp-layout-color0);
}

.lm-CommandPalette-item.lm-mod-active:hover:not(.lm-mod-disabled) {
  color: var(--jp-ui-inverse-font-color1);
  background: var(--jp-brand-color1);
}

.lm-CommandPalette-item:hover:not(.lm-mod-active):not(.lm-mod-disabled) {
  background: var(--jp-layout-color2);
}

.lm-CommandPalette-itemContent {
  overflow: hidden;
}

.lm-CommandPalette-itemLabel > mark {
  color: var(--jp-ui-font-color0);
  background-color: transparent;
  font-weight: bold;
}

.lm-CommandPalette-item.lm-mod-disabled mark {
  color: var(--jp-ui-font-color2);
}

.lm-CommandPalette-item .lm-CommandPalette-itemIcon {
  margin: 0 4px 0 0;
  position: relative;
  width: 16px;
  top: 2px;
  flex: 0 0 auto;
}

.lm-CommandPalette-item.lm-mod-disabled .lm-CommandPalette-itemIcon {
  opacity: 0.6;
}

.lm-CommandPalette-item .lm-CommandPalette-itemShortcut {
  flex: 0 0 auto;
}

.lm-CommandPalette-itemCaption {
  display: none;
}

.lm-CommandPalette-content {
  background-color: var(--jp-layout-color1);
}

.lm-CommandPalette-content:empty::after {
  content: 'No results';
  margin: auto;
  margin-top: 20px;
  width: 100px;
  display: block;
  font-size: var(--jp-ui-font-size2);
  font-family: var(--jp-ui-font-family);
  font-weight: lighter;
}

.lm-CommandPalette-emptyMessage {
  text-align: center;
  margin-top: 24px;
  line-height: 1.32;
  padding: 0 8px;
  color: var(--jp-content-font-color3);
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-Dialog {
  position: absolute;
  z-index: 10000;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  top: 0;
  left: 0;
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100%;
  background: var(--jp-dialog-background);
}

.jp-Dialog-content {
  display: flex;
  flex-direction: column;
  margin-left: auto;
  margin-right: auto;
  background: var(--jp-layout-color1);
  padding: 24px 24px 12px;
  min-width: 300px;
  min-height: 150px;
  max-width: 1000px;
  max-height: 500px;
  box-sizing: border-box;
  box-shadow: var(--jp-elevation-z20);
  word-wrap: break-word;
  border-radius: var(--jp-border-radius);

  /* This is needed so that all font sizing of children done in ems is
   * relative to this base size */
  font-size: var(--jp-ui-font-size1);
  color: var(--jp-ui-font-color1);
  resize: both;
}

.jp-Dialog-content.jp-Dialog-content-small {
  max-width: 500px;
}

.jp-Dialog-button {
  overflow: visible;
}

button.jp-Dialog-button:focus {
  outline: 1px solid var(--jp-brand-color1);
  outline-offset: 4px;
  -moz-outline-radius: 0;
}

button.jp-Dialog-button:focus::-moz-focus-inner {
  border: 0;
}

button.jp-Dialog-button.jp-mod-styled.jp-mod-accept:focus,
button.jp-Dialog-button.jp-mod-styled.jp-mod-warn:focus,
button.jp-Dialog-button.jp-mod-styled.jp-mod-reject:focus {
  outline-offset: 4px;
  -moz-outline-radius: 0;
}

button.jp-Dialog-button.jp-mod-styled.jp-mod-accept:focus {
  outline: 1px solid var(--jp-accept-color-normal, var(--jp-brand-color1));
}

button.jp-Dialog-button.jp-mod-styled.jp-mod-warn:focus {
  outline: 1px solid var(--jp-warn-color-normal, var(--jp-error-color1));
}

button.jp-Dialog-button.jp-mod-styled.jp-mod-reject:focus {
  outline: 1px solid var(--jp-reject-color-normal, var(--md-grey-600));
}

button.jp-Dialog-close-button {
  padding: 0;
  height: 100%;
  min-width: unset;
  min-height: unset;
}

.jp-Dialog-header {
  display: flex;
  justify-content: space-between;
  flex: 0 0 auto;
  padding-bottom: 12px;
  font-size: var(--jp-ui-font-size3);
  font-weight: 400;
  color: var(--jp-ui-font-color1);
}

.jp-Dialog-body {
  display: flex;
  flex-direction: column;
  flex: 1 1 auto;
  font-size: var(--jp-ui-font-size1);
  background: var(--jp-layout-color1);
  color: var(--jp-ui-font-color1);
  overflow: auto;
}

.jp-Dialog-footer {
  display: flex;
  flex-direction: row;
  justify-content: flex-end;
  align-items: center;
  flex: 0 0 auto;
  margin-left: -12px;
  margin-right: -12px;
  padding: 12px;
}

.jp-Dialog-checkbox {
  padding-right: 5px;
}

.jp-Dialog-checkbox > input:focus-visible {
  outline: 1px solid var(--jp-input-active-border-color);
  outline-offset: 1px;
}

.jp-Dialog-spacer {
  flex: 1 1 auto;
}

.jp-Dialog-title {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}

.jp-Dialog-body > .jp-select-wrapper {
  width: 100%;
}

.jp-Dialog-body > button {
  padding: 0 16px;
}

.jp-Dialog-body > label {
  line-height: 1.4;
  color: var(--jp-ui-font-color0);
}

.jp-Dialog-button.jp-mod-styled:not(:last-child) {
  margin-right: 12px;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

.jp-Input-Boolean-Dialog {
  flex-direction: row-reverse;
  align-items: end;
  width: 100%;
}

.jp-Input-Boolean-Dialog > label {
  flex: 1 1 auto;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2016, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-MainAreaWidget > :focus {
  outline: none;
}

.jp-MainAreaWidget .jp-MainAreaWidget-error {
  padding: 6px;
}

.jp-MainAreaWidget .jp-MainAreaWidget-error > pre {
  width: auto;
  padding: 10px;
  background: var(--jp-error-color3);
  border: var(--jp-border-width) solid var(--jp-error-color1);
  border-radius: var(--jp-border-radius);
  color: var(--jp-ui-font-color1);
  font-size: var(--jp-ui-font-size1);
  white-space: pre-wrap;
  word-wrap: break-word;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/**
 * google-material-color v1.2.6
 * https://github.com/danlevan/google-material-color
 */
:root {
  --md-red-50: #ffebee;
  --md-red-100: #ffcdd2;
  --md-red-200: #ef9a9a;
  --md-red-300: #e57373;
  --md-red-400: #ef5350;
  --md-red-500: #f44336;
  --md-red-600: #e53935;
  --md-red-700: #d32f2f;
  --md-red-800: #c62828;
  --md-red-900: #b71c1c;
  --md-red-A100: #ff8a80;
  --md-red-A200: #ff5252;
  --md-red-A400: #ff1744;
  --md-red-A700: #d50000;
  --md-pink-50: #fce4ec;
  --md-pink-100: #f8bbd0;
  --md-pink-200: #f48fb1;
  --md-pink-300: #f06292;
  --md-pink-400: #ec407a;
  --md-pink-500: #e91e63;
  --md-pink-600: #d81b60;
  --md-pink-700: #c2185b;
  --md-pink-800: #ad1457;
  --md-pink-900: #880e4f;
  --md-pink-A100: #ff80ab;
  --md-pink-A200: #ff4081;
  --md-pink-A400: #f50057;
  --md-pink-A700: #c51162;
  --md-purple-50: #f3e5f5;
  --md-purple-100: #e1bee7;
  --md-purple-200: #ce93d8;
  --md-purple-300: #ba68c8;
  --md-purple-400: #ab47bc;
  --md-purple-500: #9c27b0;
  --md-purple-600: #8e24aa;
  --md-purple-700: #7b1fa2;
  --md-purple-800: #6a1b9a;
  --md-purple-900: #4a148c;
  --md-purple-A100: #ea80fc;
  --md-purple-A200: #e040fb;
  --md-purple-A400: #d500f9;
  --md-purple-A700: #a0f;
  --md-deep-purple-50: #ede7f6;
  --md-deep-purple-100: #d1c4e9;
  --md-deep-purple-200: #b39ddb;
  --md-deep-purple-300: #9575cd;
  --md-deep-purple-400: #7e57c2;
  --md-deep-purple-500: #673ab7;
  --md-deep-purple-600: #5e35b1;
  --md-deep-purple-700: #512da8;
  --md-deep-purple-800: #4527a0;
  --md-deep-purple-900: #311b92;
  --md-deep-purple-A100: #b388ff;
  --md-deep-purple-A200: #7c4dff;
  --md-deep-purple-A400: #651fff;
  --md-deep-purple-A700: #6200ea;
  --md-indigo-50: #e8eaf6;
  --md-indigo-100: #c5cae9;
  --md-indigo-200: #9fa8da;
  --md-indigo-300: #7986cb;
  --md-indigo-400: #5c6bc0;
  --md-indigo-500: #3f51b5;
  --md-indigo-600: #3949ab;
  --md-indigo-700: #303f9f;
  --md-indigo-800: #283593;
  --md-indigo-900: #1a237e;
  --md-indigo-A100: #8c9eff;
  --md-indigo-A200: #536dfe;
  --md-indigo-A400: #3d5afe;
  --md-indigo-A700: #304ffe;
  --md-blue-50: #e3f2fd;
  --md-blue-100: #bbdefb;
  --md-blue-200: #90caf9;
  --md-blue-300: #64b5f6;
  --md-blue-400: #42a5f5;
  --md-blue-500: #2196f3;
  --md-blue-600: #1e88e5;
  --md-blue-700: #1976d2;
  --md-blue-800: #1565c0;
  --md-blue-900: #0d47a1;
  --md-blue-A100: #82b1ff;
  --md-blue-A200: #448aff;
  --md-blue-A400: #2979ff;
  --md-blue-A700: #2962ff;
  --md-light-blue-50: #e1f5fe;
  --md-light-blue-100: #b3e5fc;
  --md-light-blue-200: #81d4fa;
  --md-light-blue-300: #4fc3f7;
  --md-light-blue-400: #29b6f6;
  --md-light-blue-500: #03a9f4;
  --md-light-blue-600: #039be5;
  --md-light-blue-700: #0288d1;
  --md-light-blue-800: #0277bd;
  --md-light-blue-900: #01579b;
  --md-light-blue-A100: #80d8ff;
  --md-light-blue-A200: #40c4ff;
  --md-light-blue-A400: #00b0ff;
  --md-light-blue-A700: #0091ea;
  --md-cyan-50: #e0f7fa;
  --md-cyan-100: #b2ebf2;
  --md-cyan-200: #80deea;
  --md-cyan-300: #4dd0e1;
  --md-cyan-400: #26c6da;
  --md-cyan-500: #00bcd4;
  --md-cyan-600: #00acc1;
  --md-cyan-700: #0097a7;
  --md-cyan-800: #00838f;
  --md-cyan-900: #006064;
  --md-cyan-A100: #84ffff;
  --md-cyan-A200: #18ffff;
  --md-cyan-A400: #00e5ff;
  --md-cyan-A700: #00b8d4;
  --md-teal-50: #e0f2f1;
  --md-teal-100: #b2dfdb;
  --md-teal-200: #80cbc4;
  --md-teal-300: #4db6ac;
  --md-teal-400: #26a69a;
  --md-teal-500: #009688;
  --md-teal-600: #00897b;
  --md-teal-700: #00796b;
  --md-teal-800: #00695c;
  --md-teal-900: #004d40;
  --md-teal-A100: #a7ffeb;
  --md-teal-A200: #64ffda;
  --md-teal-A400: #1de9b6;
  --md-teal-A700: #00bfa5;
  --md-green-50: #e8f5e9;
  --md-green-100: #c8e6c9;
  --md-green-200: #a5d6a7;
  --md-green-300: #81c784;
  --md-green-400: #66bb6a;
  --md-green-500: #4caf50;
  --md-green-600: #43a047;
  --md-green-700: #388e3c;
  --md-green-800: #2e7d32;
  --md-green-900: #1b5e20;
  --md-green-A100: #b9f6ca;
  --md-green-A200: #69f0ae;
  --md-green-A400: #00e676;
  --md-green-A700: #00c853;
  --md-light-green-50: #f1f8e9;
  --md-light-green-100: #dcedc8;
  --md-light-green-200: #c5e1a5;
  --md-light-green-300: #aed581;
  --md-light-green-400: #9ccc65;
  --md-light-green-500: #8bc34a;
  --md-light-green-600: #7cb342;
  --md-light-green-700: #689f38;
  --md-light-green-800: #558b2f;
  --md-light-green-900: #33691e;
  --md-light-green-A100: #ccff90;
  --md-light-green-A200: #b2ff59;
  --md-light-green-A400: #76ff03;
  --md-light-green-A700: #64dd17;
  --md-lime-50: #f9fbe7;
  --md-lime-100: #f0f4c3;
  --md-lime-200: #e6ee9c;
  --md-lime-300: #dce775;
  --md-lime-400: #d4e157;
  --md-lime-500: #cddc39;
  --md-lime-600: #c0ca33;
  --md-lime-700: #afb42b;
  --md-lime-800: #9e9d24;
  --md-lime-900: #827717;
  --md-lime-A100: #f4ff81;
  --md-lime-A200: #eeff41;
  --md-lime-A400: #c6ff00;
  --md-lime-A700: #aeea00;
  --md-yellow-50: #fffde7;
  --md-yellow-100: #fff9c4;
  --md-yellow-200: #fff59d;
  --md-yellow-300: #fff176;
  --md-yellow-400: #ffee58;
  --md-yellow-500: #ffeb3b;
  --md-yellow-600: #fdd835;
  --md-yellow-700: #fbc02d;
  --md-yellow-800: #f9a825;
  --md-yellow-900: #f57f17;
  --md-yellow-A100: #ffff8d;
  --md-yellow-A200: #ff0;
  --md-yellow-A400: #ffea00;
  --md-yellow-A700: #ffd600;
  --md-amber-50: #fff8e1;
  --md-amber-100: #ffecb3;
  --md-amber-200: #ffe082;
  --md-amber-300: #ffd54f;
  --md-amber-400: #ffca28;
  --md-amber-500: #ffc107;
  --md-amber-600: #ffb300;
  --md-amber-700: #ffa000;
  --md-amber-800: #ff8f00;
  --md-amber-900: #ff6f00;
  --md-amber-A100: #ffe57f;
  --md-amber-A200: #ffd740;
  --md-amber-A400: #ffc400;
  --md-amber-A700: #ffab00;
  --md-orange-50: #fff3e0;
  --md-orange-100: #ffe0b2;
  --md-orange-200: #ffcc80;
  --md-orange-300: #ffb74d;
  --md-orange-400: #ffa726;
  --md-orange-500: #ff9800;
  --md-orange-600: #fb8c00;
  --md-orange-700: #f57c00;
  --md-orange-800: #ef6c00;
  --md-orange-900: #e65100;
  --md-orange-A100: #ffd180;
  --md-orange-A200: #ffab40;
  --md-orange-A400: #ff9100;
  --md-orange-A700: #ff6d00;
  --md-deep-orange-50: #fbe9e7;
  --md-deep-orange-100: #ffccbc;
  --md-deep-orange-200: #ffab91;
  --md-deep-orange-300: #ff8a65;
  --md-deep-orange-400: #ff7043;
  --md-deep-orange-500: #ff5722;
  --md-deep-orange-600: #f4511e;
  --md-deep-orange-700: #e64a19;
  --md-deep-orange-800: #d84315;
  --md-deep-orange-900: #bf360c;
  --md-deep-orange-A100: #ff9e80;
  --md-deep-orange-A200: #ff6e40;
  --md-deep-orange-A400: #ff3d00;
  --md-deep-orange-A700: #dd2c00;
  --md-brown-50: #efebe9;
  --md-brown-100: #d7ccc8;
  --md-brown-200: #bcaaa4;
  --md-brown-300: #a1887f;
  --md-brown-400: #8d6e63;
  --md-brown-500: #795548;
  --md-brown-600: #6d4c41;
  --md-brown-700: #5d4037;
  --md-brown-800: #4e342e;
  --md-brown-900: #3e2723;
  --md-grey-50: #fafafa;
  --md-grey-100: #f5f5f5;
  --md-grey-200: #eee;
  --md-grey-300: #e0e0e0;
  --md-grey-400: #bdbdbd;
  --md-grey-500: #9e9e9e;
  --md-grey-600: #757575;
  --md-grey-700: #616161;
  --md-grey-800: #424242;
  --md-grey-900: #212121;
  --md-blue-grey-50: #eceff1;
  --md-blue-grey-100: #cfd8dc;
  --md-blue-grey-200: #b0bec5;
  --md-blue-grey-300: #90a4ae;
  --md-blue-grey-400: #78909c;
  --md-blue-grey-500: #607d8b;
  --md-blue-grey-600: #546e7a;
  --md-blue-grey-700: #455a64;
  --md-blue-grey-800: #37474f;
  --md-blue-grey-900: #263238;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| RenderedText
|----------------------------------------------------------------------------*/

:root {
  /* This is the padding value to fill the gaps between lines containing spans with background color. */
  --jp-private-code-span-padding: calc(
    (var(--jp-code-line-height) - 1) * var(--jp-code-font-size) / 2
  );
}

.jp-RenderedText {
  text-align: left;
  padding-left: var(--jp-code-padding);
  line-height: var(--jp-code-line-height);
  font-family: var(--jp-code-font-family);
}

.jp-RenderedText pre,
.jp-RenderedJavaScript pre,
.jp-RenderedHTMLCommon pre {
  color: var(--jp-content-font-color1);
  font-size: var(--jp-code-font-size);
  border: none;
  margin: 0;
  padding: 0;
}

.jp-RenderedText pre a:link {
  text-decoration: none;
  color: var(--jp-content-link-color);
}

.jp-RenderedText pre a:hover {
  text-decoration: underline;
  color: var(--jp-content-link-color);
}

.jp-RenderedText pre a:visited {
  text-decoration: none;
  color: var(--jp-content-link-color);
}

/* console foregrounds and backgrounds */
.jp-RenderedText pre .ansi-black-fg {
  color: #3e424d;
}

.jp-RenderedText pre .ansi-red-fg {
  color: #e75c58;
}

.jp-RenderedText pre .ansi-green-fg {
  color: #00a250;
}

.jp-RenderedText pre .ansi-yellow-fg {
  color: #ddb62b;
}

.jp-RenderedText pre .ansi-blue-fg {
  color: #208ffb;
}

.jp-RenderedText pre .ansi-magenta-fg {
  color: #d160c4;
}

.jp-RenderedText pre .ansi-cyan-fg {
  color: #60c6c8;
}

.jp-RenderedText pre .ansi-white-fg {
  color: #c5c1b4;
}

.jp-RenderedText pre .ansi-black-bg {
  background-color: #3e424d;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-red-bg {
  background-color: #e75c58;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-green-bg {
  background-color: #00a250;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-yellow-bg {
  background-color: #ddb62b;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-blue-bg {
  background-color: #208ffb;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-magenta-bg {
  background-color: #d160c4;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-cyan-bg {
  background-color: #60c6c8;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-white-bg {
  background-color: #c5c1b4;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-black-intense-fg {
  color: #282c36;
}

.jp-RenderedText pre .ansi-red-intense-fg {
  color: #b22b31;
}

.jp-RenderedText pre .ansi-green-intense-fg {
  color: #007427;
}

.jp-RenderedText pre .ansi-yellow-intense-fg {
  color: #b27d12;
}

.jp-RenderedText pre .ansi-blue-intense-fg {
  color: #0065ca;
}

.jp-RenderedText pre .ansi-magenta-intense-fg {
  color: #a03196;
}

.jp-RenderedText pre .ansi-cyan-intense-fg {
  color: #258f8f;
}

.jp-RenderedText pre .ansi-white-intense-fg {
  color: #a1a6b2;
}

.jp-RenderedText pre .ansi-black-intense-bg {
  background-color: #282c36;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-red-intense-bg {
  background-color: #b22b31;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-green-intense-bg {
  background-color: #007427;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-yellow-intense-bg {
  background-color: #b27d12;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-blue-intense-bg {
  background-color: #0065ca;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-magenta-intense-bg {
  background-color: #a03196;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-cyan-intense-bg {
  background-color: #258f8f;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-white-intense-bg {
  background-color: #a1a6b2;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-default-inverse-fg {
  color: var(--jp-ui-inverse-font-color0);
}

.jp-RenderedText pre .ansi-default-inverse-bg {
  background-color: var(--jp-inverse-layout-color0);
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-bold {
  font-weight: bold;
}

.jp-RenderedText pre .ansi-underline {
  text-decoration: underline;
}

.jp-RenderedText[data-mime-type='application/vnd.jupyter.stderr'] {
  background: var(--jp-rendermime-error-background);
  padding-top: var(--jp-code-padding);
}

/*-----------------------------------------------------------------------------
| RenderedLatex
|----------------------------------------------------------------------------*/

.jp-RenderedLatex {
  color: var(--jp-content-font-color1);
  font-size: var(--jp-content-font-size1);
  line-height: var(--jp-content-line-height);
}

/* Left-justify outputs.*/
.jp-OutputArea-output.jp-RenderedLatex {
  padding: var(--jp-code-padding);
  text-align: left;
}

/*-----------------------------------------------------------------------------
| RenderedHTML
|----------------------------------------------------------------------------*/

.jp-RenderedHTMLCommon {
  color: var(--jp-content-font-color1);
  font-family: var(--jp-content-font-family);
  font-size: var(--jp-content-font-size1);
  line-height: var(--jp-content-line-height);

  /* Give a bit more R padding on Markdown text to keep line lengths reasonable */
  padding-right: 20px;
}

.jp-RenderedHTMLCommon em {
  font-style: italic;
}

.jp-RenderedHTMLCommon strong {
  font-weight: bold;
}

.jp-RenderedHTMLCommon u {
  text-decoration: underline;
}

.jp-RenderedHTMLCommon a:link {
  text-decoration: none;
  color: var(--jp-content-link-color);
}

.jp-RenderedHTMLCommon a:hover {
  text-decoration: underline;
  color: var(--jp-content-link-color);
}

.jp-RenderedHTMLCommon a:visited {
  text-decoration: none;
  color: var(--jp-content-link-color);
}

/* Headings */

.jp-RenderedHTMLCommon h1,
.jp-RenderedHTMLCommon h2,
.jp-RenderedHTMLCommon h3,
.jp-RenderedHTMLCommon h4,
.jp-RenderedHTMLCommon h5,
.jp-RenderedHTMLCommon h6 {
  line-height: var(--jp-content-heading-line-height);
  font-weight: var(--jp-content-heading-font-weight);
  font-style: normal;
  margin: var(--jp-content-heading-margin-top) 0
    var(--jp-content-heading-margin-bottom) 0;
}

.jp-RenderedHTMLCommon h1:first-child,
.jp-RenderedHTMLCommon h2:first-child,
.jp-RenderedHTMLCommon h3:first-child,
.jp-RenderedHTMLCommon h4:first-child,
.jp-RenderedHTMLCommon h5:first-child,
.jp-RenderedHTMLCommon h6:first-child {
  margin-top: calc(0.5 * var(--jp-content-heading-margin-top));
}

.jp-RenderedHTMLCommon h1:last-child,
.jp-RenderedHTMLCommon h2:last-child,
.jp-RenderedHTMLCommon h3:last-child,
.jp-RenderedHTMLCommon h4:last-child,
.jp-RenderedHTMLCommon h5:last-child,
.jp-RenderedHTMLCommon h6:last-child {
  margin-bottom: calc(0.5 * var(--jp-content-heading-margin-bottom));
}

.jp-RenderedHTMLCommon h1 {
  font-size: var(--jp-content-font-size5);
}

.jp-RenderedHTMLCommon h2 {
  font-size: var(--jp-content-font-size4);
}

.jp-RenderedHTMLCommon h3 {
  font-size: var(--jp-content-font-size3);
}

.jp-RenderedHTMLCommon h4 {
  font-size: var(--jp-content-font-size2);
}

.jp-RenderedHTMLCommon h5 {
  font-size: var(--jp-content-font-size1);
}

.jp-RenderedHTMLCommon h6 {
  font-size: var(--jp-content-font-size0);
}

/* Lists */

/* stylelint-disable selector-max-type, selector-max-compound-selectors */

.jp-RenderedHTMLCommon ul:not(.list-inline),
.jp-RenderedHTMLCommon ol:not(.list-inline) {
  padding-left: 2em;
}

.jp-RenderedHTMLCommon ul {
  list-style: disc;
}

.jp-RenderedHTMLCommon ul ul {
  list-style: square;
}

.jp-RenderedHTMLCommon ul ul ul {
  list-style: circle;
}

.jp-RenderedHTMLCommon ol {
  list-style: decimal;
}

.jp-RenderedHTMLCommon ol ol {
  list-style: upper-alpha;
}

.jp-RenderedHTMLCommon ol ol ol {
  list-style: lower-alpha;
}

.jp-RenderedHTMLCommon ol ol ol ol {
  list-style: lower-roman;
}

.jp-RenderedHTMLCommon ol ol ol ol ol {
  list-style: decimal;
}

.jp-RenderedHTMLCommon ol,
.jp-RenderedHTMLCommon ul {
  margin-bottom: 1em;
}

.jp-RenderedHTMLCommon ul ul,
.jp-RenderedHTMLCommon ul ol,
.jp-RenderedHTMLCommon ol ul,
.jp-RenderedHTMLCommon ol ol {
  margin-bottom: 0;
}

/* stylelint-enable selector-max-type, selector-max-compound-selectors */

.jp-RenderedHTMLCommon hr {
  color: var(--jp-border-color2);
  background-color: var(--jp-border-color1);
  margin-top: 1em;
  margin-bottom: 1em;
}

.jp-RenderedHTMLCommon > pre {
  margin: 1.5em 2em;
}

.jp-RenderedHTMLCommon pre,
.jp-RenderedHTMLCommon code {
  border: 0;
  background-color: var(--jp-layout-color0);
  color: var(--jp-content-font-color1);
  font-family: var(--jp-code-font-family);
  font-size: inherit;
  line-height: var(--jp-code-line-height);
  padding: 0;
  white-space: pre-wrap;
}

.jp-RenderedHTMLCommon :not(pre) > code {
  background-color: var(--jp-layout-color2);
  padding: 1px 5px;
}

/* Tables */

.jp-RenderedHTMLCommon table {
  border-collapse: collapse;
  border-spacing: 0;
  border: none;
  color: var(--jp-ui-font-color1);
  font-size: var(--jp-ui-font-size1);
  table-layout: fixed;
  margin-left: auto;
  margin-bottom: 1em;
  margin-right: auto;
}

.jp-RenderedHTMLCommon thead {
  border-bottom: var(--jp-border-width) solid var(--jp-border-color1);
  vertical-align: bottom;
}

.jp-RenderedHTMLCommon td,
.jp-RenderedHTMLCommon th,
.jp-RenderedHTMLCommon tr {
  vertical-align: middle;
  padding: 0.5em;
  line-height: normal;
  white-space: normal;
  max-width: none;
  border: none;
}

.jp-RenderedMarkdown.jp-RenderedHTMLCommon td,
.jp-RenderedMarkdown.jp-RenderedHTMLCommon th {
  max-width: none;
}

:not(.jp-RenderedMarkdown).jp-RenderedHTMLCommon td,
:not(.jp-RenderedMarkdown).jp-RenderedHTMLCommon th,
:not(.jp-RenderedMarkdown).jp-RenderedHTMLCommon tr {
  text-align: right;
}

.jp-RenderedHTMLCommon th {
  font-weight: bold;
}

.jp-RenderedHTMLCommon tbody tr:nth-child(odd) {
  background: var(--jp-layout-color0);
}

.jp-RenderedHTMLCommon tbody tr:nth-child(even) {
  background: var(--jp-rendermime-table-row-background);
}

.jp-RenderedHTMLCommon tbody tr:hover {
  background: var(--jp-rendermime-table-row-hover-background);
}

.jp-RenderedHTMLCommon p {
  text-align: left;
  margin: 0;
  margin-bottom: 1em;
}

.jp-RenderedHTMLCommon img {
  -moz-force-broken-image-icon: 1;
}

/* Restrict to direct children as other images could be nested in other content. */
.jp-RenderedHTMLCommon > img {
  display: block;
  margin-left: 0;
  margin-right: 0;
  margin-bottom: 1em;
}

/* Change color behind transparent images if they need it... */
[data-jp-theme-light='false'] .jp-RenderedImage img.jp-needs-light-background {
  background-color: var(--jp-inverse-layout-color1);
}

[data-jp-theme-light='true'] .jp-RenderedImage img.jp-needs-dark-background {
  background-color: var(--jp-inverse-layout-color1);
}

.jp-RenderedHTMLCommon img,
.jp-RenderedImage img,
.jp-RenderedHTMLCommon svg,
.jp-RenderedSVG svg {
  max-width: 100%;
  height: auto;
}

.jp-RenderedHTMLCommon img.jp-mod-unconfined,
.jp-RenderedImage img.jp-mod-unconfined,
.jp-RenderedHTMLCommon svg.jp-mod-unconfined,
.jp-RenderedSVG svg.jp-mod-unconfined {
  max-width: none;
}

.jp-RenderedHTMLCommon .alert {
  padding: var(--jp-notebook-padding);
  border: var(--jp-border-width) solid transparent;
  border-radius: var(--jp-border-radius);
  margin-bottom: 1em;
}

.jp-RenderedHTMLCommon .alert-info {
  color: var(--jp-info-color0);
  background-color: var(--jp-info-color3);
  border-color: var(--jp-info-color2);
}

.jp-RenderedHTMLCommon .alert-info hr {
  border-color: var(--jp-info-color3);
}

.jp-RenderedHTMLCommon .alert-info > p:last-child,
.jp-RenderedHTMLCommon .alert-info > ul:last-child {
  margin-bottom: 0;
}

.jp-RenderedHTMLCommon .alert-warning {
  color: var(--jp-warn-color0);
  background-color: var(--jp-warn-color3);
  border-color: var(--jp-warn-color2);
}

.jp-RenderedHTMLCommon .alert-warning hr {
  border-color: var(--jp-warn-color3);
}

.jp-RenderedHTMLCommon .alert-warning > p:last-child,
.jp-RenderedHTMLCommon .alert-warning > ul:last-child {
  margin-bottom: 0;
}

.jp-RenderedHTMLCommon .alert-success {
  color: var(--jp-success-color0);
  background-color: var(--jp-success-color3);
  border-color: var(--jp-success-color2);
}

.jp-RenderedHTMLCommon .alert-success hr {
  border-color: var(--jp-success-color3);
}

.jp-RenderedHTMLCommon .alert-success > p:last-child,
.jp-RenderedHTMLCommon .alert-success > ul:last-child {
  margin-bottom: 0;
}

.jp-RenderedHTMLCommon .alert-danger {
  color: var(--jp-error-color0);
  background-color: var(--jp-error-color3);
  border-color: var(--jp-error-color2);
}

.jp-RenderedHTMLCommon .alert-danger hr {
  border-color: var(--jp-error-color3);
}

.jp-RenderedHTMLCommon .alert-danger > p:last-child,
.jp-RenderedHTMLCommon .alert-danger > ul:last-child {
  margin-bottom: 0;
}

.jp-RenderedHTMLCommon blockquote {
  margin: 1em 2em;
  padding: 0 1em;
  border-left: 5px solid var(--jp-border-color2);
}

a.jp-InternalAnchorLink {
  visibility: hidden;
  margin-left: 8px;
  color: var(--md-blue-800);
}

h1:hover .jp-InternalAnchorLink,
h2:hover .jp-InternalAnchorLink,
h3:hover .jp-InternalAnchorLink,
h4:hover .jp-InternalAnchorLink,
h5:hover .jp-InternalAnchorLink,
h6:hover .jp-InternalAnchorLink {
  visibility: visible;
}

.jp-RenderedHTMLCommon kbd {
  background-color: var(--jp-rendermime-table-row-background);
  border: 1px solid var(--jp-border-color0);
  border-bottom-color: var(--jp-border-color2);
  border-radius: 3px;
  box-shadow: inset 0 -1px 0 rgba(0, 0, 0, 0.25);
  display: inline-block;
  font-size: var(--jp-ui-font-size0);
  line-height: 1em;
  padding: 0.2em 0.5em;
}

/* Most direct children of .jp-RenderedHTMLCommon have a margin-bottom of 1.0.
 * At the bottom of cells this is a bit too much as there is also spacing
 * between cells. Going all the way to 0 gets too tight between markdown and
 * code cells.
 */
.jp-RenderedHTMLCommon > *:last-child {
  margin-bottom: 0.5em;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-cursor-backdrop {
  position: fixed;
  width: 200px;
  height: 200px;
  margin-top: -100px;
  margin-left: -100px;
  will-change: transform;
  z-index: 100;
}

.lm-mod-drag-image {
  will-change: transform;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

.jp-lineFormSearch {
  padding: 4px 12px;
  background-color: var(--jp-layout-color2);
  box-shadow: var(--jp-toolbar-box-shadow);
  z-index: 2;
  font-size: var(--jp-ui-font-size1);
}

.jp-lineFormCaption {
  font-size: var(--jp-ui-font-size0);
  line-height: var(--jp-ui-font-size1);
  margin-top: 4px;
  color: var(--jp-ui-font-color0);
}

.jp-baseLineForm {
  border: none;
  border-radius: 0;
  position: absolute;
  background-size: 16px;
  background-repeat: no-repeat;
  background-position: center;
  outline: none;
}

.jp-lineFormButtonContainer {
  top: 4px;
  right: 8px;
  height: 24px;
  padding: 0 12px;
  width: 12px;
}

.jp-lineFormButtonIcon {
  top: 0;
  right: 0;
  background-color: var(--jp-brand-color1);
  height: 100%;
  width: 100%;
  box-sizing: border-box;
  padding: 4px 6px;
}

.jp-lineFormButton {
  top: 0;
  right: 0;
  background-color: transparent;
  height: 100%;
  width: 100%;
  box-sizing: border-box;
}

.jp-lineFormWrapper {
  overflow: hidden;
  padding: 0 8px;
  border: 1px solid var(--jp-border-color0);
  background-color: var(--jp-input-active-background);
  height: 22px;
}

.jp-lineFormWrapperFocusWithin {
  border: var(--jp-border-width) solid var(--md-blue-500);
  box-shadow: inset 0 0 4px var(--md-blue-300);
}

.jp-lineFormInput {
  background: transparent;
  width: 200px;
  height: 100%;
  border: none;
  outline: none;
  color: var(--jp-ui-font-color0);
  line-height: 28px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2016, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-JSONEditor {
  display: flex;
  flex-direction: column;
  width: 100%;
}

.jp-JSONEditor-host {
  flex: 1 1 auto;
  border: var(--jp-border-width) solid var(--jp-input-border-color);
  border-radius: 0;
  background: var(--jp-layout-color0);
  min-height: 50px;
  padding: 1px;
}

.jp-JSONEditor.jp-mod-error .jp-JSONEditor-host {
  border-color: red;
  outline-color: red;
}

.jp-JSONEditor-header {
  display: flex;
  flex: 1 0 auto;
  padding: 0 0 0 12px;
}

.jp-JSONEditor-header label {
  flex: 0 0 auto;
}

.jp-JSONEditor-commitButton {
  height: 16px;
  width: 16px;
  background-size: 18px;
  background-repeat: no-repeat;
  background-position: center;
}

.jp-JSONEditor-host.jp-mod-focused {
  background-color: var(--jp-input-active-background);
  border: 1px solid var(--jp-input-active-border-color);
  box-shadow: var(--jp-input-box-shadow);
}

.jp-Editor.jp-mod-dropTarget {
  border: var(--jp-border-width) solid var(--jp-input-active-border-color);
  box-shadow: var(--jp-input-box-shadow);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/
.jp-DocumentSearch-input {
  border: none;
  outline: none;
  color: var(--jp-ui-font-color0);
  font-size: var(--jp-ui-font-size1);
  background-color: var(--jp-layout-color0);
  font-family: var(--jp-ui-font-family);
  padding: 2px 1px;
  resize: none;
}

.jp-DocumentSearch-overlay {
  position: absolute;
  background-color: var(--jp-toolbar-background);
  border-bottom: var(--jp-border-width) solid var(--jp-toolbar-border-color);
  border-left: var(--jp-border-width) solid var(--jp-toolbar-border-color);
  top: 0;
  right: 0;
  z-index: 7;
  min-width: 405px;
  padding: 2px;
  font-size: var(--jp-ui-font-size1);

  --jp-private-document-search-button-height: 20px;
}

.jp-DocumentSearch-overlay button {
  background-color: var(--jp-toolbar-background);
  outline: 0;
}

.jp-DocumentSearch-overlay button:hover {
  background-color: var(--jp-layout-color2);
}

.jp-DocumentSearch-overlay button:active {
  background-color: var(--jp-layout-color3);
}

.jp-DocumentSearch-overlay-row {
  display: flex;
  align-items: center;
  margin-bottom: 2px;
}

.jp-DocumentSearch-button-content {
  display: inline-block;
  cursor: pointer;
  box-sizing: border-box;
  width: 100%;
  height: 100%;
}

.jp-DocumentSearch-button-content svg {
  width: 100%;
  height: 100%;
}

.jp-DocumentSearch-input-wrapper {
  border: var(--jp-border-width) solid var(--jp-border-color0);
  display: flex;
  background-color: var(--jp-layout-color0);
  margin: 2px;
}

.jp-DocumentSearch-input-wrapper:focus-within {
  border-color: var(--jp-cell-editor-active-border-color);
}

.jp-DocumentSearch-toggle-wrapper,
.jp-DocumentSearch-button-wrapper {
  all: initial;
  overflow: hidden;
  display: inline-block;
  border: none;
  box-sizing: border-box;
}

.jp-DocumentSearch-toggle-wrapper {
  width: 14px;
  height: 14px;
}

.jp-DocumentSearch-button-wrapper {
  width: var(--jp-private-document-search-button-height);
  height: var(--jp-private-document-search-button-height);
}

.jp-DocumentSearch-toggle-wrapper:focus,
.jp-DocumentSearch-button-wrapper:focus {
  outline: var(--jp-border-width) solid
    var(--jp-cell-editor-active-border-color);
  outline-offset: -1px;
}

.jp-DocumentSearch-toggle-wrapper,
.jp-DocumentSearch-button-wrapper,
.jp-DocumentSearch-button-content:focus {
  outline: none;
}

.jp-DocumentSearch-toggle-placeholder {
  width: 5px;
}

.jp-DocumentSearch-input-button::before {
  display: block;
  padding-top: 100%;
}

.jp-DocumentSearch-input-button-off {
  opacity: var(--jp-search-toggle-off-opacity);
}

.jp-DocumentSearch-input-button-off:hover {
  opacity: var(--jp-search-toggle-hover-opacity);
}

.jp-DocumentSearch-input-button-on {
  opacity: var(--jp-search-toggle-on-opacity);
}

.jp-DocumentSearch-index-counter {
  padding-left: 10px;
  padding-right: 10px;
  user-select: none;
  min-width: 35px;
  display: inline-block;
}

.jp-DocumentSearch-up-down-wrapper {
  display: inline-block;
  padding-right: 2px;
  margin-left: auto;
  white-space: nowrap;
}

.jp-DocumentSearch-spacer {
  margin-left: auto;
}

.jp-DocumentSearch-up-down-wrapper button {
  outline: 0;
  border: none;
  width: var(--jp-private-document-search-button-height);
  height: var(--jp-private-document-search-button-height);
  vertical-align: middle;
  margin: 1px 5px 2px;
}

.jp-DocumentSearch-up-down-button:hover {
  background-color: var(--jp-layout-color2);
}

.jp-DocumentSearch-up-down-button:active {
  background-color: var(--jp-layout-color3);
}

.jp-DocumentSearch-filter-button {
  border-radius: var(--jp-border-radius);
}

.jp-DocumentSearch-filter-button:hover {
  background-color: var(--jp-layout-color2);
}

.jp-DocumentSearch-filter-button-enabled {
  background-color: var(--jp-layout-color2);
}

.jp-DocumentSearch-filter-button-enabled:hover {
  background-color: var(--jp-layout-color3);
}

.jp-DocumentSearch-search-options {
  padding: 0 8px;
  margin-left: 3px;
  width: 100%;
  display: grid;
  justify-content: start;
  grid-template-columns: 1fr 1fr;
  align-items: center;
  justify-items: stretch;
}

.jp-DocumentSearch-search-filter-disabled {
  color: var(--jp-ui-font-color2);
}

.jp-DocumentSearch-search-filter {
  display: flex;
  align-items: center;
  user-select: none;
}

.jp-DocumentSearch-regex-error {
  color: var(--jp-error-color0);
}

.jp-DocumentSearch-replace-button-wrapper {
  overflow: hidden;
  display: inline-block;
  box-sizing: border-box;
  border: var(--jp-border-width) solid var(--jp-border-color0);
  margin: auto 2px;
  padding: 1px 4px;
  height: calc(var(--jp-private-document-search-button-height) + 2px);
}

.jp-DocumentSearch-replace-button-wrapper:focus {
  border: var(--jp-border-width) solid var(--jp-cell-editor-active-border-color);
}

.jp-DocumentSearch-replace-button {
  display: inline-block;
  text-align: center;
  cursor: pointer;
  box-sizing: border-box;
  color: var(--jp-ui-font-color1);

  /* height - 2 * (padding of wrapper) */
  line-height: calc(var(--jp-private-document-search-button-height) - 2px);
  width: 100%;
  height: 100%;
}

.jp-DocumentSearch-replace-button:focus {
  outline: none;
}

.jp-DocumentSearch-replace-wrapper-class {
  margin-left: 14px;
  display: flex;
}

.jp-DocumentSearch-replace-toggle {
  border: none;
  background-color: var(--jp-toolbar-background);
  border-radius: var(--jp-border-radius);
}

.jp-DocumentSearch-replace-toggle:hover {
  background-color: var(--jp-layout-color2);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.cm-editor {
  line-height: var(--jp-code-line-height);
  font-size: var(--jp-code-font-size);
  font-family: var(--jp-code-font-family);
  border: 0;
  border-radius: 0;
  height: auto;

  /* Changed to auto to autogrow */
}

.cm-editor pre {
  padding: 0 var(--jp-code-padding);
}

.jp-CodeMirrorEditor[data-type='inline'] .cm-dialog {
  background-color: var(--jp-layout-color0);
  color: var(--jp-content-font-color1);
}

.jp-CodeMirrorEditor {
  cursor: text;
}

/* When zoomed out 67% and 33% on a screen of 1440 width x 900 height */
@media screen and (min-width: 2138px) and (max-width: 4319px) {
  .jp-CodeMirrorEditor[data-type='inline'] .cm-cursor {
    border-left: var(--jp-code-cursor-width1) solid
      var(--jp-editor-cursor-color);
  }
}

/* When zoomed out less than 33% */
@media screen and (min-width: 4320px) {
  .jp-CodeMirrorEditor[data-type='inline'] .cm-cursor {
    border-left: var(--jp-code-cursor-width2) solid
      var(--jp-editor-cursor-color);
  }
}

.cm-editor.jp-mod-readOnly .cm-cursor {
  display: none;
}

.jp-CollaboratorCursor {
  border-left: 5px solid transparent;
  border-right: 5px solid transparent;
  border-top: none;
  border-bottom: 3px solid;
  background-clip: content-box;
  margin-left: -5px;
  margin-right: -5px;
}

.cm-searching,
.cm-searching span {
  /* `.cm-searching span`: we need to override syntax highlighting */
  background-color: var(--jp-search-unselected-match-background-color);
  color: var(--jp-search-unselected-match-color);
}

.cm-searching::selection,
.cm-searching span::selection {
  background-color: var(--jp-search-unselected-match-background-color);
  color: var(--jp-search-unselected-match-color);
}

.jp-current-match > .cm-searching,
.jp-current-match > .cm-searching span,
.cm-searching > .jp-current-match,
.cm-searching > .jp-current-match span {
  background-color: var(--jp-search-selected-match-background-color);
  color: var(--jp-search-selected-match-color);
}

.jp-current-match > .cm-searching::selection,
.cm-searching > .jp-current-match::selection,
.jp-current-match > .cm-searching span::selection {
  background-color: var(--jp-search-selected-match-background-color);
  color: var(--jp-search-selected-match-color);
}

.cm-trailingspace {
  background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAgAAAAFCAYAAAB4ka1VAAAAsElEQVQIHQGlAFr/AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA7+r3zKmT0/+pk9P/7+r3zAAAAAAAAAAABAAAAAAAAAAA6OPzM+/q9wAAAAAA6OPzMwAAAAAAAAAAAgAAAAAAAAAAGR8NiRQaCgAZIA0AGR8NiQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAQyoYJ/SY80UAAAAASUVORK5CYII=);
  background-position: center left;
  background-repeat: repeat-x;
}

.jp-CollaboratorCursor-hover {
  position: absolute;
  z-index: 1;
  transform: translateX(-50%);
  color: white;
  border-radius: 3px;
  padding-left: 4px;
  padding-right: 4px;
  padding-top: 1px;
  padding-bottom: 1px;
  text-align: center;
  font-size: var(--jp-ui-font-size1);
  white-space: nowrap;
}

.jp-CodeMirror-ruler {
  border-left: 1px dashed var(--jp-border-color2);
}

/* Styles for shared cursors (remote cursor locations and selected ranges) */
.jp-CodeMirrorEditor .cm-ySelectionCaret {
  position: relative;
  border-left: 1px solid black;
  margin-left: -1px;
  margin-right: -1px;
  box-sizing: border-box;
}

.jp-CodeMirrorEditor .cm-ySelectionCaret > .cm-ySelectionInfo {
  white-space: nowrap;
  position: absolute;
  top: -1.15em;
  padding-bottom: 0.05em;
  left: -1px;
  font-size: 0.95em;
  font-family: var(--jp-ui-font-family);
  font-weight: bold;
  line-height: normal;
  user-select: none;
  color: white;
  padding-left: 2px;
  padding-right: 2px;
  z-index: 101;
  transition: opacity 0.3s ease-in-out;
}

.jp-CodeMirrorEditor .cm-ySelectionInfo {
  transition-delay: 0.7s;
  opacity: 0;
}

.jp-CodeMirrorEditor .cm-ySelectionCaret:hover > .cm-ySelectionInfo {
  opacity: 1;
  transition-delay: 0s;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-MimeDocument {
  outline: none;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Variables
|----------------------------------------------------------------------------*/

:root {
  --jp-private-filebrowser-button-height: 28px;
  --jp-private-filebrowser-button-width: 48px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-FileBrowser .jp-SidePanel-content {
  display: flex;
  flex-direction: column;
}

.jp-FileBrowser-toolbar.jp-Toolbar {
  flex-wrap: wrap;
  row-gap: 12px;
  border-bottom: none;
  height: auto;
  margin: 8px 12px 0;
  box-shadow: none;
  padding: 0;
  justify-content: flex-start;
}

.jp-FileBrowser-Panel {
  flex: 1 1 auto;
  display: flex;
  flex-direction: column;
}

.jp-BreadCrumbs {
  flex: 0 0 auto;
  margin: 8px 12px;
}

.jp-BreadCrumbs-item {
  margin: 0 2px;
  padding: 0 2px;
  border-radius: var(--jp-border-radius);
  cursor: pointer;
}

.jp-BreadCrumbs-item:hover {
  background-color: var(--jp-layout-color2);
}

.jp-BreadCrumbs-item:first-child {
  margin-left: 0;
}

.jp-BreadCrumbs-item.jp-mod-dropTarget {
  background-color: var(--jp-brand-color2);
  opacity: 0.7;
}

/*-----------------------------------------------------------------------------
| Buttons
|----------------------------------------------------------------------------*/

.jp-FileBrowser-toolbar > .jp-Toolbar-item {
  flex: 0 0 auto;
  padding-left: 0;
  padding-right: 2px;
  align-items: center;
  height: unset;
}

.jp-FileBrowser-toolbar > .jp-Toolbar-item .jp-ToolbarButtonComponent {
  width: 40px;
}

/*-----------------------------------------------------------------------------
| Other styles
|----------------------------------------------------------------------------*/

.jp-FileDialog.jp-mod-conflict input {
  color: var(--jp-error-color1);
}

.jp-FileDialog .jp-new-name-title {
  margin-top: 12px;
}

.jp-LastModified-hidden {
  display: none;
}

.jp-FileSize-hidden {
  display: none;
}

.jp-FileBrowser .lm-AccordionPanel > h3:first-child {
  display: none;
}

/*-----------------------------------------------------------------------------
| DirListing
|----------------------------------------------------------------------------*/

.jp-DirListing {
  flex: 1 1 auto;
  display: flex;
  flex-direction: column;
  outline: 0;
}

.jp-DirListing-header {
  flex: 0 0 auto;
  display: flex;
  flex-direction: row;
  align-items: center;
  overflow: hidden;
  border-top: var(--jp-border-width) solid var(--jp-border-color2);
  border-bottom: var(--jp-border-width) solid var(--jp-border-color1);
  box-shadow: var(--jp-toolbar-box-shadow);
  z-index: 2;
}

.jp-DirListing-headerItem {
  padding: 4px 12px 2px;
  font-weight: 500;
}

.jp-DirListing-headerItem:hover {
  background: var(--jp-layout-color2);
}

.jp-DirListing-headerItem.jp-id-name {
  flex: 1 0 84px;
}

.jp-DirListing-headerItem.jp-id-modified {
  flex: 0 0 112px;
  border-left: var(--jp-border-width) solid var(--jp-border-color2);
  text-align: right;
}

.jp-DirListing-headerItem.jp-id-filesize {
  flex: 0 0 75px;
  border-left: var(--jp-border-width) solid var(--jp-border-color2);
  text-align: right;
}

.jp-id-narrow {
  display: none;
  flex: 0 0 5px;
  padding: 4px;
  border-left: var(--jp-border-width) solid var(--jp-border-color2);
  text-align: right;
  color: var(--jp-border-color2);
}

.jp-DirListing-narrow .jp-id-narrow {
  display: block;
}

.jp-DirListing-narrow .jp-id-modified,
.jp-DirListing-narrow .jp-DirListing-itemModified {
  display: none;
}

.jp-DirListing-headerItem.jp-mod-selected {
  font-weight: 600;
}

/* increase specificity to override bundled default */
.jp-DirListing-content {
  flex: 1 1 auto;
  margin: 0;
  padding: 0;
  list-style-type: none;
  overflow: auto;
  background-color: var(--jp-layout-color1);
}

.jp-DirListing-content mark {
  color: var(--jp-ui-font-color0);
  background-color: transparent;
  font-weight: bold;
}

.jp-DirListing-content .jp-DirListing-item.jp-mod-selected mark {
  color: var(--jp-ui-inverse-font-color0);
}

/* Style the directory listing content when a user drops a file to upload */
.jp-DirListing.jp-mod-native-drop .jp-DirListing-content {
  outline: 5px dashed rgba(128, 128, 128, 0.5);
  outline-offset: -10px;
  cursor: copy;
}

.jp-DirListing-item {
  display: flex;
  flex-direction: row;
  align-items: center;
  padding: 4px 12px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.jp-DirListing-checkboxWrapper {
  /* Increases hit area of checkbox. */
  padding: 4px;
}

.jp-DirListing-header
  .jp-DirListing-checkboxWrapper
  + .jp-DirListing-headerItem {
  padding-left: 4px;
}

.jp-DirListing-content .jp-DirListing-checkboxWrapper {
  position: relative;
  left: -4px;
  margin: -4px 0 -4px -8px;
}

.jp-DirListing-checkboxWrapper.jp-mod-visible {
  visibility: visible;
}

/* For devices that support hovering, hide checkboxes until hovered, selected...
*/
@media (hover: hover) {
  .jp-DirListing-checkboxWrapper {
    visibility: hidden;
  }

  .jp-DirListing-item:hover .jp-DirListing-checkboxWrapper,
  .jp-DirListing-item.jp-mod-selected .jp-DirListing-checkboxWrapper {
    visibility: visible;
  }
}

.jp-DirListing-item[data-is-dot] {
  opacity: 75%;
}

.jp-DirListing-item.jp-mod-selected {
  color: var(--jp-ui-inverse-font-color1);
  background: var(--jp-brand-color1);
}

.jp-DirListing-item.jp-mod-dropTarget {
  background: var(--jp-brand-color3);
}

.jp-DirListing-item:hover:not(.jp-mod-selected) {
  background: var(--jp-layout-color2);
}

.jp-DirListing-itemIcon {
  flex: 0 0 20px;
  margin-right: 4px;
}

.jp-DirListing-itemText {
  flex: 1 0 64px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  user-select: none;
}

.jp-DirListing-itemText:focus {
  outline-width: 2px;
  outline-color: var(--jp-inverse-layout-color1);
  outline-style: solid;
  outline-offset: 1px;
}

.jp-DirListing-item.jp-mod-selected .jp-DirListing-itemText:focus {
  outline-color: var(--jp-layout-color1);
}

.jp-DirListing-itemModified {
  flex: 0 0 125px;
  text-align: right;
}

.jp-DirListing-itemFileSize {
  flex: 0 0 90px;
  text-align: right;
}

.jp-DirListing-editor {
  flex: 1 0 64px;
  outline: none;
  border: none;
  color: var(--jp-ui-font-color1);
  background-color: var(--jp-layout-color1);
}

.jp-DirListing-item.jp-mod-running .jp-DirListing-itemIcon::before {
  color: var(--jp-success-color1);
  content: '\25CF';
  font-size: 8px;
  position: absolute;
  left: -8px;
}

.jp-DirListing-item.jp-mod-running.jp-mod-selected
  .jp-DirListing-itemIcon::before {
  color: var(--jp-ui-inverse-font-color1);
}

.jp-DirListing-item.lm-mod-drag-image,
.jp-DirListing-item.jp-mod-selected.lm-mod-drag-image {
  font-size: var(--jp-ui-font-size1);
  padding-left: 4px;
  margin-left: 4px;
  width: 160px;
  background-color: var(--jp-ui-inverse-font-color2);
  box-shadow: var(--jp-elevation-z2);
  border-radius: 0;
  color: var(--jp-ui-font-color1);
  transform: translateX(-40%) translateY(-58%);
}

.jp-Document {
  min-width: 120px;
  min-height: 120px;
  outline: none;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Main OutputArea
| OutputArea has a list of Outputs
|----------------------------------------------------------------------------*/

.jp-OutputArea {
  overflow-y: auto;
}

.jp-OutputArea-child {
  display: table;
  table-layout: fixed;
  width: 100%;
  overflow: hidden;
}

.jp-OutputPrompt {
  width: var(--jp-cell-prompt-width);
  color: var(--jp-cell-outprompt-font-color);
  font-family: var(--jp-cell-prompt-font-family);
  padding: var(--jp-code-padding);
  letter-spacing: var(--jp-cell-prompt-letter-spacing);
  line-height: var(--jp-code-line-height);
  font-size: var(--jp-code-font-size);
  border: var(--jp-border-width) solid transparent;
  opacity: var(--jp-cell-prompt-opacity);

  /* Right align prompt text, don't wrap to handle large prompt numbers */
  text-align: right;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;

  /* Disable text selection */
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.jp-OutputArea-prompt {
  display: table-cell;
  vertical-align: top;
}

.jp-OutputArea-output {
  display: table-cell;
  width: 100%;
  height: auto;
  overflow: auto;
  user-select: text;
  -moz-user-select: text;
  -webkit-user-select: text;
  -ms-user-select: text;
}

.jp-OutputArea .jp-RenderedText {
  padding-left: 1ch;
}

/**
 * Prompt overlay.
 */

.jp-OutputArea-promptOverlay {
  position: absolute;
  top: 0;
  width: var(--jp-cell-prompt-width);
  height: 100%;
  opacity: 0.5;
}

.jp-OutputArea-promptOverlay:hover {
  background: var(--jp-layout-color2);
  box-shadow: inset 0 0 1px var(--jp-inverse-layout-color0);
  cursor: zoom-out;
}

.jp-mod-outputsScrolled .jp-OutputArea-promptOverlay:hover {
  cursor: zoom-in;
}

/**
 * Isolated output.
 */
.jp-OutputArea-output.jp-mod-isolated {
  width: 100%;
  display: block;
}

/*
When drag events occur, `lm-mod-override-cursor` is added to the body.
Because iframes steal all cursor events, the following two rules are necessary
to suppress pointer events while resize drags are occurring. There may be a
better solution to this problem.
*/
body.lm-mod-override-cursor .jp-OutputArea-output.jp-mod-isolated {
  position: relative;
}

body.lm-mod-override-cursor .jp-OutputArea-output.jp-mod-isolated::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: transparent;
}

/* pre */

.jp-OutputArea-output pre {
  border: none;
  margin: 0;
  padding: 0;
  overflow-x: auto;
  overflow-y: auto;
  word-break: break-all;
  word-wrap: break-word;
  white-space: pre-wrap;
}

/* tables */

.jp-OutputArea-output.jp-RenderedHTMLCommon table {
  margin-left: 0;
  margin-right: 0;
}

/* description lists */

.jp-OutputArea-output dl,
.jp-OutputArea-output dt,
.jp-OutputArea-output dd {
  display: block;
}

.jp-OutputArea-output dl {
  width: 100%;
  overflow: hidden;
  padding: 0;
  margin: 0;
}

.jp-OutputArea-output dt {
  font-weight: bold;
  float: left;
  width: 20%;
  padding: 0;
  margin: 0;
}

.jp-OutputArea-output dd {
  float: left;
  width: 80%;
  padding: 0;
  margin: 0;
}

.jp-TrimmedOutputs pre {
  background: var(--jp-layout-color3);
  font-size: calc(var(--jp-code-font-size) * 1.4);
  text-align: center;
  text-transform: uppercase;
}

/* Hide the gutter in case of
 *  - nested output areas (e.g. in the case of output widgets)
 *  - mirrored output areas
 */
.jp-OutputArea .jp-OutputArea .jp-OutputArea-prompt {
  display: none;
}

/* Hide empty lines in the output area, for instance due to cleared widgets */
.jp-OutputArea-prompt:empty {
  padding: 0;
  border: 0;
}

/*-----------------------------------------------------------------------------
| executeResult is added to any Output-result for the display of the object
| returned by a cell
|----------------------------------------------------------------------------*/

.jp-OutputArea-output.jp-OutputArea-executeResult {
  margin-left: 0;
  width: 100%;
}

/* Text output with the Out[] prompt needs a top padding to match the
 * alignment of the Out[] prompt itself.
 */
.jp-OutputArea-executeResult .jp-RenderedText.jp-OutputArea-output {
  padding-top: var(--jp-code-padding);
  border-top: var(--jp-border-width) solid transparent;
}

/*-----------------------------------------------------------------------------
| The Stdin output
|----------------------------------------------------------------------------*/

.jp-Stdin-prompt {
  color: var(--jp-content-font-color0);
  padding-right: var(--jp-code-padding);
  vertical-align: baseline;
  flex: 0 0 auto;
}

.jp-Stdin-input {
  font-family: var(--jp-code-font-family);
  font-size: inherit;
  color: inherit;
  background-color: inherit;
  width: 42%;
  min-width: 200px;

  /* make sure input baseline aligns with prompt */
  vertical-align: baseline;

  /* padding + margin = 0.5em between prompt and cursor */
  padding: 0 0.25em;
  margin: 0 0.25em;
  flex: 0 0 70%;
}

.jp-Stdin-input::placeholder {
  opacity: 0;
}

.jp-Stdin-input:focus {
  box-shadow: none;
}

.jp-Stdin-input:focus::placeholder {
  opacity: 1;
}

/*-----------------------------------------------------------------------------
| Output Area View
|----------------------------------------------------------------------------*/

.jp-LinkedOutputView .jp-OutputArea {
  height: 100%;
  display: block;
}

.jp-LinkedOutputView .jp-OutputArea-output:only-child {
  height: 100%;
}

/*-----------------------------------------------------------------------------
| Printing
|----------------------------------------------------------------------------*/

@media print {
  .jp-OutputArea-child {
    break-inside: avoid-page;
  }
}

/*-----------------------------------------------------------------------------
| Mobile
|----------------------------------------------------------------------------*/
@media only screen and (max-width: 760px) {
  .jp-OutputPrompt {
    display: table-row;
    text-align: left;
  }

  .jp-OutputArea-child .jp-OutputArea-output {
    display: table-row;
    margin-left: var(--jp-notebook-padding);
  }
}

/* Trimmed outputs warning */
.jp-TrimmedOutputs > a {
  margin: 10px;
  text-decoration: none;
  cursor: pointer;
}

.jp-TrimmedOutputs > a:hover {
  text-decoration: none;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Table of Contents
|----------------------------------------------------------------------------*/

:root {
  --jp-private-toc-active-width: 4px;
}

.jp-TableOfContents {
  display: flex;
  flex-direction: column;
  background: var(--jp-layout-color1);
  color: var(--jp-ui-font-color1);
  font-size: var(--jp-ui-font-size1);
  height: 100%;
}

.jp-TableOfContents-placeholder {
  text-align: center;
}

.jp-TableOfContents-placeholderContent {
  color: var(--jp-content-font-color2);
  padding: 8px;
}

.jp-TableOfContents-placeholderContent > h3 {
  margin-bottom: var(--jp-content-heading-margin-bottom);
}

.jp-TableOfContents .jp-SidePanel-content {
  overflow-y: auto;
}

.jp-TableOfContents-tree {
  margin: 4px;
}

.jp-TableOfContents ol {
  list-style-type: none;
}

/* stylelint-disable-next-line selector-max-type */
.jp-TableOfContents li > ol {
  /* Align left border with triangle icon center */
  padding-left: 11px;
}

.jp-TableOfContents-content {
  /* left margin for the active heading indicator */
  margin: 0 0 0 var(--jp-private-toc-active-width);
  padding: 0;
  background-color: var(--jp-layout-color1);
}

.jp-tocItem {
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.jp-tocItem-heading {
  display: flex;
  cursor: pointer;
}

.jp-tocItem-heading:hover {
  background-color: var(--jp-layout-color2);
}

.jp-tocItem-content {
  display: block;
  padding: 4px 0;
  white-space: nowrap;
  text-overflow: ellipsis;
  overflow-x: hidden;
}

.jp-tocItem-collapser {
  height: 20px;
  margin: 2px 2px 0;
  padding: 0;
  background: none;
  border: none;
  cursor: pointer;
}

.jp-tocItem-collapser:hover {
  background-color: var(--jp-layout-color3);
}

/* Active heading indicator */

.jp-tocItem-heading::before {
  content: ' ';
  background: transparent;
  width: var(--jp-private-toc-active-width);
  height: 24px;
  position: absolute;
  left: 0;
  border-radius: var(--jp-border-radius);
}

.jp-tocItem-heading.jp-tocItem-active::before {
  background-color: var(--jp-brand-color1);
}

.jp-tocItem-heading:hover.jp-tocItem-active::before {
  background: var(--jp-brand-color0);
  opacity: 1;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-Collapser {
  flex: 0 0 var(--jp-cell-collapser-width);
  padding: 0;
  margin: 0;
  border: none;
  outline: none;
  background: transparent;
  border-radius: var(--jp-border-radius);
  opacity: 1;
}

.jp-Collapser-child {
  display: block;
  width: 100%;
  box-sizing: border-box;

  /* height: 100% doesn't work because the height of its parent is computed from content */
  position: absolute;
  top: 0;
  bottom: 0;
}

/*-----------------------------------------------------------------------------
| Printing
|----------------------------------------------------------------------------*/

/*
Hiding collapsers in print mode.

Note: input and output wrappers have "display: block" propery in print mode.
*/

@media print {
  .jp-Collapser {
    display: none;
  }
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Header/Footer
|----------------------------------------------------------------------------*/

/* Hidden by zero height by default */
.jp-CellHeader,
.jp-CellFooter {
  height: 0;
  width: 100%;
  padding: 0;
  margin: 0;
  border: none;
  outline: none;
  background: transparent;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Input
|----------------------------------------------------------------------------*/

/* All input areas */
.jp-InputArea {
  display: table;
  table-layout: fixed;
  width: 100%;
  overflow: hidden;
}

.jp-InputArea-editor {
  display: table-cell;
  overflow: hidden;
  vertical-align: top;

  /* This is the non-active, default styling */
  border: var(--jp-border-width) solid var(--jp-cell-editor-border-color);
  border-radius: 0;
  background: var(--jp-cell-editor-background);
}

.jp-InputPrompt {
  display: table-cell;
  vertical-align: top;
  width: var(--jp-cell-prompt-width);
  color: var(--jp-cell-inprompt-font-color);
  font-family: var(--jp-cell-prompt-font-family);
  padding: var(--jp-code-padding);
  letter-spacing: var(--jp-cell-prompt-letter-spacing);
  opacity: var(--jp-cell-prompt-opacity);
  line-height: var(--jp-code-line-height);
  font-size: var(--jp-code-font-size);
  border: var(--jp-border-width) solid transparent;

  /* Right align prompt text, don't wrap to handle large prompt numbers */
  text-align: right;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;

  /* Disable text selection */
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

/*-----------------------------------------------------------------------------
| Mobile
|----------------------------------------------------------------------------*/
@media only screen and (max-width: 760px) {
  .jp-InputArea-editor {
    display: table-row;
    margin-left: var(--jp-notebook-padding);
  }

  .jp-InputPrompt {
    display: table-row;
    text-align: left;
  }
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Placeholder
|----------------------------------------------------------------------------*/

.jp-Placeholder {
  display: table;
  table-layout: fixed;
  width: 100%;
}

.jp-Placeholder-prompt {
  display: table-cell;
  box-sizing: border-box;
}

.jp-Placeholder-content {
  display: table-cell;
  padding: 4px 6px;
  border: 1px solid transparent;
  border-radius: 0;
  background: none;
  box-sizing: border-box;
  cursor: pointer;
}

.jp-Placeholder-contentContainer {
  display: flex;
}

.jp-Placeholder-content:hover,
.jp-InputPlaceholder > .jp-Placeholder-content:hover {
  border-color: var(--jp-layout-color3);
}

.jp-Placeholder-content .jp-MoreHorizIcon {
  width: 32px;
  height: 16px;
  border: 1px solid transparent;
  border-radius: var(--jp-border-radius);
}

.jp-Placeholder-content .jp-MoreHorizIcon:hover {
  border: 1px solid var(--jp-border-color1);
  box-shadow: 0 0 2px 0 rgba(0, 0, 0, 0.25);
  background-color: var(--jp-layout-color0);
}

.jp-PlaceholderText {
  white-space: nowrap;
  overflow-x: hidden;
  color: var(--jp-inverse-layout-color3);
  font-family: var(--jp-code-font-family);
}

.jp-InputPlaceholder > .jp-Placeholder-content {
  border-color: var(--jp-cell-editor-border-color);
  background: var(--jp-cell-editor-background);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Private CSS variables
|----------------------------------------------------------------------------*/

:root {
  --jp-private-cell-scrolling-output-offset: 5px;
}

/*-----------------------------------------------------------------------------
| Cell
|----------------------------------------------------------------------------*/

.jp-Cell {
  padding: var(--jp-cell-padding);
  margin: 0;
  border: none;
  outline: none;
  background: transparent;
}

/*-----------------------------------------------------------------------------
| Common input/output
|----------------------------------------------------------------------------*/

.jp-Cell-inputWrapper,
.jp-Cell-outputWrapper {
  display: flex;
  flex-direction: row;
  padding: 0;
  margin: 0;

  /* Added to reveal the box-shadow on the input and output collapsers. */
  overflow: visible;
}

/* Only input/output areas inside cells */
.jp-Cell-inputArea,
.jp-Cell-outputArea {
  flex: 1 1 auto;
}

/*-----------------------------------------------------------------------------
| Collapser
|----------------------------------------------------------------------------*/

/* Make the output collapser disappear when there is not output, but do so
 * in a manner that leaves it in the layout and preserves its width.
 */
.jp-Cell.jp-mod-noOutputs .jp-Cell-outputCollapser {
  border: none !important;
  background: transparent !important;
}

.jp-Cell:not(.jp-mod-noOutputs) .jp-Cell-outputCollapser {
  min-height: var(--jp-cell-collapser-min-height);
}

/*-----------------------------------------------------------------------------
| Output
|----------------------------------------------------------------------------*/

/* Put a space between input and output when there IS output */
.jp-Cell:not(.jp-mod-noOutputs) .jp-Cell-outputWrapper {
  margin-top: 5px;
}

.jp-CodeCell.jp-mod-outputsScrolled .jp-Cell-outputArea {
  overflow-y: auto;
  max-height: 24em;
  margin-left: var(--jp-private-cell-scrolling-output-offset);
  resize: vertical;
}

.jp-CodeCell.jp-mod-outputsScrolled .jp-Cell-outputArea[style*='height'] {
  max-height: unset;
}

.jp-CodeCell.jp-mod-outputsScrolled .jp-Cell-outputArea::after {
  content: ' ';
  box-shadow: inset 0 0 6px 2px rgb(0 0 0 / 30%);
  width: 100%;
  height: 100%;
  position: sticky;
  bottom: 0;
  top: 0;
  margin-top: -50%;
  float: left;
  display: block;
  pointer-events: none;
}

.jp-CodeCell.jp-mod-outputsScrolled .jp-OutputArea-child {
  padding-top: 6px;
}

.jp-CodeCell.jp-mod-outputsScrolled .jp-OutputArea-prompt {
  width: calc(
    var(--jp-cell-prompt-width) - var(--jp-private-cell-scrolling-output-offset)
  );
}

.jp-CodeCell.jp-mod-outputsScrolled .jp-OutputArea-promptOverlay {
  left: calc(-1 * var(--jp-private-cell-scrolling-output-offset));
}

/*-----------------------------------------------------------------------------
| CodeCell
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| MarkdownCell
|----------------------------------------------------------------------------*/

.jp-MarkdownOutput {
  display: table-cell;
  width: 100%;
  margin-top: 0;
  margin-bottom: 0;
  padding-left: var(--jp-code-padding);
}

.jp-MarkdownOutput.jp-RenderedHTMLCommon {
  overflow: auto;
}

/* collapseHeadingButton (show always if hiddenCellsButton is _not_ shown) */
.jp-collapseHeadingButton {
  display: flex;
  min-height: var(--jp-cell-collapser-min-height);
  font-size: var(--jp-code-font-size);
  position: absolute;
  background-color: transparent;
  background-size: 25px;
  background-repeat: no-repeat;
  background-position-x: center;
  background-position-y: top;
  background-image: var(--jp-icon-caret-down);
  right: 0;
  top: 0;
  bottom: 0;
}

.jp-collapseHeadingButton.jp-mod-collapsed {
  background-image: var(--jp-icon-caret-right);
}

/*
 set the container font size to match that of content
 so that the nested collapse buttons have the right size
*/
.jp-MarkdownCell .jp-InputPrompt {
  font-size: var(--jp-content-font-size1);
}

/*
  Align collapseHeadingButton with cell top header
  The font sizes are identical to the ones in packages/rendermime/style/base.css
*/
.jp-mod-rendered .jp-collapseHeadingButton[data-heading-level='1'] {
  font-size: var(--jp-content-font-size5);
  background-position-y: calc(0.3 * var(--jp-content-font-size5));
}

.jp-mod-rendered .jp-collapseHeadingButton[data-heading-level='2'] {
  font-size: var(--jp-content-font-size4);
  background-position-y: calc(0.3 * var(--jp-content-font-size4));
}

.jp-mod-rendered .jp-collapseHeadingButton[data-heading-level='3'] {
  font-size: var(--jp-content-font-size3);
  background-position-y: calc(0.3 * var(--jp-content-font-size3));
}

.jp-mod-rendered .jp-collapseHeadingButton[data-heading-level='4'] {
  font-size: var(--jp-content-font-size2);
  background-position-y: calc(0.3 * var(--jp-content-font-size2));
}

.jp-mod-rendered .jp-collapseHeadingButton[data-heading-level='5'] {
  font-size: var(--jp-content-font-size1);
  background-position-y: top;
}

.jp-mod-rendered .jp-collapseHeadingButton[data-heading-level='6'] {
  font-size: var(--jp-content-font-size0);
  background-position-y: top;
}

/* collapseHeadingButton (show only on (hover,active) if hiddenCellsButton is shown) */
.jp-Notebook.jp-mod-showHiddenCellsButton .jp-collapseHeadingButton {
  display: none;
}

.jp-Notebook.jp-mod-showHiddenCellsButton
  :is(.jp-MarkdownCell:hover, .jp-mod-active)
  .jp-collapseHeadingButton {
  display: flex;
}

/* showHiddenCellsButton (only show if jp-mod-showHiddenCellsButton is set, which
is a consequence of the showHiddenCellsButton option in Notebook Settings)*/
.jp-Notebook.jp-mod-showHiddenCellsButton .jp-showHiddenCellsButton {
  margin-left: calc(var(--jp-cell-prompt-width) + 2 * var(--jp-code-padding));
  margin-top: var(--jp-code-padding);
  border: 1px solid var(--jp-border-color2);
  background-color: var(--jp-border-color3) !important;
  color: var(--jp-content-font-color0) !important;
  display: flex;
}

.jp-Notebook.jp-mod-showHiddenCellsButton .jp-showHiddenCellsButton:hover {
  background-color: var(--jp-border-color2) !important;
}

.jp-showHiddenCellsButton {
  display: none;
}

/*-----------------------------------------------------------------------------
| Printing
|----------------------------------------------------------------------------*/

/*
Using block instead of flex to allow the use of the break-inside CSS property for
cell outputs.
*/

@media print {
  .jp-Cell-inputWrapper,
  .jp-Cell-outputWrapper {
    display: block;
  }
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Variables
|----------------------------------------------------------------------------*/

:root {
  --jp-notebook-toolbar-padding: 2px 5px 2px 2px;
}

/*-----------------------------------------------------------------------------

/*-----------------------------------------------------------------------------
| Styles
|----------------------------------------------------------------------------*/

.jp-NotebookPanel-toolbar {
  padding: var(--jp-notebook-toolbar-padding);

  /* disable paint containment from lumino 2.0 default strict CSS containment */
  contain: style size !important;
}

.jp-Toolbar-item.jp-Notebook-toolbarCellType .jp-select-wrapper.jp-mod-focused {
  border: none;
  box-shadow: none;
}

.jp-Notebook-toolbarCellTypeDropdown select {
  height: 24px;
  font-size: var(--jp-ui-font-size1);
  line-height: 14px;
  border-radius: 0;
  display: block;
}

.jp-Notebook-toolbarCellTypeDropdown span {
  top: 5px !important;
}

.jp-Toolbar-responsive-popup {
  position: absolute;
  height: fit-content;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: flex-end;
  border-bottom: var(--jp-border-width) solid var(--jp-toolbar-border-color);
  box-shadow: var(--jp-toolbar-box-shadow);
  background: var(--jp-toolbar-background);
  min-height: var(--jp-toolbar-micro-height);
  padding: var(--jp-notebook-toolbar-padding);
  z-index: 1;
  right: 0;
  top: 0;
}

.jp-Toolbar > .jp-Toolbar-responsive-opener {
  margin-left: auto;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Variables
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------

/*-----------------------------------------------------------------------------
| Styles
|----------------------------------------------------------------------------*/

.jp-Notebook-ExecutionIndicator {
  position: relative;
  display: inline-block;
  height: 100%;
  z-index: 9997;
}

.jp-Notebook-ExecutionIndicator-tooltip {
  visibility: hidden;
  height: auto;
  width: max-content;
  width: -moz-max-content;
  background-color: var(--jp-layout-color2);
  color: var(--jp-ui-font-color1);
  text-align: justify;
  border-radius: 6px;
  padding: 0 5px;
  position: fixed;
  display: table;
}

.jp-Notebook-ExecutionIndicator-tooltip.up {
  transform: translateX(-50%) translateY(-100%) translateY(-32px);
}

.jp-Notebook-ExecutionIndicator-tooltip.down {
  transform: translateX(calc(-100% + 16px)) translateY(5px);
}

.jp-Notebook-ExecutionIndicator-tooltip.hidden {
  display: none;
}

.jp-Notebook-ExecutionIndicator:hover .jp-Notebook-ExecutionIndicator-tooltip {
  visibility: visible;
}

.jp-Notebook-ExecutionIndicator span {
  font-size: var(--jp-ui-font-size1);
  font-family: var(--jp-ui-font-family);
  color: var(--jp-ui-font-color1);
  line-height: 24px;
  display: block;
}

.jp-Notebook-ExecutionIndicator-progress-bar {
  display: flex;
  justify-content: center;
  height: 100%;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*
 * Execution indicator
 */
.jp-tocItem-content::after {
  content: '';

  /* Must be identical to form a circle */
  width: 12px;
  height: 12px;
  background: none;
  border: none;
  position: absolute;
  right: 0;
}

.jp-tocItem-content[data-running='0']::after {
  border-radius: 50%;
  border: var(--jp-border-width) solid var(--jp-inverse-layout-color3);
  background: none;
}

.jp-tocItem-content[data-running='1']::after {
  border-radius: 50%;
  border: var(--jp-border-width) solid var(--jp-inverse-layout-color3);
  background-color: var(--jp-inverse-layout-color3);
}

.jp-tocItem-content[data-running='0'],
.jp-tocItem-content[data-running='1'] {
  margin-right: 12px;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

.jp-Notebook-footer {
  height: 27px;
  margin-left: calc(
    var(--jp-cell-prompt-width) + var(--jp-cell-collapser-width) +
      var(--jp-cell-padding)
  );
  width: calc(
    100% -
      (
        var(--jp-cell-prompt-width) + var(--jp-cell-collapser-width) +
          var(--jp-cell-padding) + var(--jp-cell-padding)
      )
  );
  border: var(--jp-border-width) solid var(--jp-cell-editor-border-color);
  color: var(--jp-ui-font-color3);
  margin-top: 6px;
  background: none;
  cursor: pointer;
}

.jp-Notebook-footer:focus {
  border-color: var(--jp-cell-editor-active-border-color);
}

/* For devices that support hovering, hide footer until hover */
@media (hover: hover) {
  .jp-Notebook-footer {
    opacity: 0;
  }

  .jp-Notebook-footer:focus,
  .jp-Notebook-footer:hover {
    opacity: 1;
  }
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Imports
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| CSS variables
|----------------------------------------------------------------------------*/

:root {
  --jp-side-by-side-output-size: 1fr;
  --jp-side-by-side-resized-cell: var(--jp-side-by-side-output-size);
  --jp-private-notebook-dragImage-width: 304px;
  --jp-private-notebook-dragImage-height: 36px;
  --jp-private-notebook-selected-color: var(--md-blue-400);
  --jp-private-notebook-active-color: var(--md-green-400);
}

/*-----------------------------------------------------------------------------
| Notebook
|----------------------------------------------------------------------------*/

/* stylelint-disable selector-max-class */

.jp-NotebookPanel {
  display: block;
  height: 100%;
}

.jp-NotebookPanel.jp-Document {
  min-width: 240px;
  min-height: 120px;
}

.jp-Notebook {
  padding: var(--jp-notebook-padding);
  outline: none;
  overflow: auto;
  background: var(--jp-layout-color0);
}

.jp-Notebook.jp-mod-scrollPastEnd::after {
  display: block;
  content: '';
  min-height: var(--jp-notebook-scroll-padding);
}

.jp-MainAreaWidget-ContainStrict .jp-Notebook * {
  contain: strict;
}

.jp-Notebook .jp-Cell {
  overflow: visible;
}

.jp-Notebook .jp-Cell .jp-InputPrompt {
  cursor: move;
}

/*-----------------------------------------------------------------------------
| Notebook state related styling
|
| The notebook and cells each have states, here are the possibilities:
|
| - Notebook
|   - Command
|   - Edit
| - Cell
|   - None
|   - Active (only one can be active)
|   - Selected (the cells actions are applied to)
|   - Multiselected (when multiple selected, the cursor)
|   - No outputs
|----------------------------------------------------------------------------*/

/* Command or edit modes */

.jp-Notebook .jp-Cell:not(.jp-mod-active) .jp-InputPrompt {
  opacity: var(--jp-cell-prompt-not-active-opacity);
  color: var(--jp-cell-prompt-not-active-font-color);
}

.jp-Notebook .jp-Cell:not(.jp-mod-active) .jp-OutputPrompt {
  opacity: var(--jp-cell-prompt-not-active-opacity);
  color: var(--jp-cell-prompt-not-active-font-color);
}

/* cell is active */
.jp-Notebook .jp-Cell.jp-mod-active .jp-Collapser {
  background: var(--jp-brand-color1);
}

/* cell is dirty */
.jp-Notebook .jp-Cell.jp-mod-dirty .jp-InputPrompt {
  color: var(--jp-warn-color1);
}

.jp-Notebook .jp-Cell.jp-mod-dirty .jp-InputPrompt::before {
  color: var(--jp-warn-color1);
  content: '•';
}

.jp-Notebook .jp-Cell.jp-mod-active.jp-mod-dirty .jp-Collapser {
  background: var(--jp-warn-color1);
}

/* collapser is hovered */
.jp-Notebook .jp-Cell .jp-Collapser:hover {
  box-shadow: var(--jp-elevation-z2);
  background: var(--jp-brand-color1);
  opacity: var(--jp-cell-collapser-not-active-hover-opacity);
}

/* cell is active and collapser is hovered */
.jp-Notebook .jp-Cell.jp-mod-active .jp-Collapser:hover {
  background: var(--jp-brand-color0);
  opacity: 1;
}

/* Command mode */

.jp-Notebook.jp-mod-commandMode .jp-Cell.jp-mod-selected {
  background: var(--jp-notebook-multiselected-color);
}

.jp-Notebook.jp-mod-commandMode
  .jp-Cell.jp-mod-active.jp-mod-selected:not(.jp-mod-multiSelected) {
  background: transparent;
}

/* Edit mode */

.jp-Notebook.jp-mod-editMode .jp-Cell.jp-mod-active .jp-InputArea-editor {
  border: var(--jp-border-width) solid var(--jp-cell-editor-active-border-color);
  box-shadow: var(--jp-input-box-shadow);
  background-color: var(--jp-cell-editor-active-background);
}

/*-----------------------------------------------------------------------------
| Notebook drag and drop
|----------------------------------------------------------------------------*/

.jp-Notebook-cell.jp-mod-dropSource {
  opacity: 0.5;
}

.jp-Notebook-cell.jp-mod-dropTarget,
.jp-Notebook.jp-mod-commandMode
  .jp-Notebook-cell.jp-mod-active.jp-mod-selected.jp-mod-dropTarget {
  border-top-color: var(--jp-private-notebook-selected-color);
  border-top-style: solid;
  border-top-width: 2px;
}

.jp-dragImage {
  display: block;
  flex-direction: row;
  width: var(--jp-private-notebook-dragImage-width);
  height: var(--jp-private-notebook-dragImage-height);
  border: var(--jp-border-width) solid var(--jp-cell-editor-border-color);
  background: var(--jp-cell-editor-background);
  overflow: visible;
}

.jp-dragImage-singlePrompt {
  box-shadow: 2px 2px 4px 0 rgba(0, 0, 0, 0.12);
}

.jp-dragImage .jp-dragImage-content {
  flex: 1 1 auto;
  z-index: 2;
  font-size: var(--jp-code-font-size);
  font-family: var(--jp-code-font-family);
  line-height: var(--jp-code-line-height);
  padding: var(--jp-code-padding);
  border: var(--jp-border-width) solid var(--jp-cell-editor-border-color);
  background: var(--jp-cell-editor-background-color);
  color: var(--jp-content-font-color3);
  text-align: left;
  margin: 4px 4px 4px 0;
}

.jp-dragImage .jp-dragImage-prompt {
  flex: 0 0 auto;
  min-width: 36px;
  color: var(--jp-cell-inprompt-font-color);
  padding: var(--jp-code-padding);
  padding-left: 12px;
  font-family: var(--jp-cell-prompt-font-family);
  letter-spacing: var(--jp-cell-prompt-letter-spacing);
  line-height: 1.9;
  font-size: var(--jp-code-font-size);
  border: var(--jp-border-width) solid transparent;
}

.jp-dragImage-multipleBack {
  z-index: -1;
  position: absolute;
  height: 32px;
  width: 300px;
  top: 8px;
  left: 8px;
  background: var(--jp-layout-color2);
  border: var(--jp-border-width) solid var(--jp-input-border-color);
  box-shadow: 2px 2px 4px 0 rgba(0, 0, 0, 0.12);
}

/*-----------------------------------------------------------------------------
| Cell toolbar
|----------------------------------------------------------------------------*/

.jp-NotebookTools {
  display: block;
  min-width: var(--jp-sidebar-min-width);
  color: var(--jp-ui-font-color1);
  background: var(--jp-layout-color1);

  /* This is needed so that all font sizing of children done in ems is
    * relative to this base size */
  font-size: var(--jp-ui-font-size1);
  overflow: auto;
}

.jp-ActiveCellTool {
  padding: 12px 0;
  display: flex;
}

.jp-ActiveCellTool-Content {
  flex: 1 1 auto;
}

.jp-ActiveCellTool .jp-ActiveCellTool-CellContent {
  background: var(--jp-cell-editor-background);
  border: var(--jp-border-width) solid var(--jp-cell-editor-border-color);
  border-radius: 0;
  min-height: 29px;
}

.jp-ActiveCellTool .jp-InputPrompt {
  min-width: calc(var(--jp-cell-prompt-width) * 0.75);
}

.jp-ActiveCellTool-CellContent > pre {
  padding: 5px 4px;
  margin: 0;
  white-space: normal;
}

.jp-MetadataEditorTool {
  flex-direction: column;
  padding: 12px 0;
}

.jp-RankedPanel > :not(:first-child) {
  margin-top: 12px;
}

.jp-KeySelector select.jp-mod-styled {
  font-size: var(--jp-ui-font-size1);
  color: var(--jp-ui-font-color0);
  border: var(--jp-border-width) solid var(--jp-border-color1);
}

.jp-KeySelector label,
.jp-MetadataEditorTool label,
.jp-NumberSetter label {
  line-height: 1.4;
}

.jp-NotebookTools .jp-select-wrapper {
  margin-top: 4px;
  margin-bottom: 0;
}

.jp-NumberSetter input {
  width: 100%;
  margin-top: 4px;
}

.jp-NotebookTools .jp-Collapse {
  margin-top: 16px;
}

/*-----------------------------------------------------------------------------
| Presentation Mode (.jp-mod-presentationMode)
|----------------------------------------------------------------------------*/

.jp-mod-presentationMode .jp-Notebook {
  --jp-content-font-size1: var(--jp-content-presentation-font-size1);
  --jp-code-font-size: var(--jp-code-presentation-font-size);
}

.jp-mod-presentationMode .jp-Notebook .jp-Cell .jp-InputPrompt,
.jp-mod-presentationMode .jp-Notebook .jp-Cell .jp-OutputPrompt {
  flex: 0 0 110px;
}

/*-----------------------------------------------------------------------------
| Side-by-side Mode (.jp-mod-sideBySide)
|----------------------------------------------------------------------------*/
.jp-mod-sideBySide.jp-Notebook .jp-Notebook-cell {
  margin-top: 3em;
  margin-bottom: 3em;
  margin-left: 5%;
  margin-right: 5%;
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell {
  display: grid;
  grid-template-columns: minmax(0, 1fr) min-content minmax(
      0,
      var(--jp-side-by-side-output-size)
    );
  grid-template-rows: auto minmax(0, 1fr) auto;
  grid-template-areas:
    'header header header'
    'input handle output'
    'footer footer footer';
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell.jp-mod-resizedCell {
  grid-template-columns: minmax(0, 1fr) min-content minmax(
      0,
      var(--jp-side-by-side-resized-cell)
    );
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell .jp-CellHeader {
  grid-area: header;
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell .jp-Cell-inputWrapper {
  grid-area: input;
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell .jp-Cell-outputWrapper {
  /* overwrite the default margin (no vertical separation needed in side by side move */
  margin-top: 0;
  grid-area: output;
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell .jp-CellFooter {
  grid-area: footer;
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell .jp-CellResizeHandle {
  grid-area: handle;
  user-select: none;
  display: block;
  height: 100%;
  cursor: ew-resize;
  padding: 0 var(--jp-cell-padding);
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell .jp-CellResizeHandle::after {
  content: '';
  display: block;
  background: var(--jp-border-color2);
  height: 100%;
  width: 5px;
}

.jp-mod-sideBySide.jp-Notebook
  .jp-CodeCell.jp-mod-resizedCell
  .jp-CellResizeHandle::after {
  background: var(--jp-border-color0);
}

.jp-CellResizeHandle {
  display: none;
}

/*-----------------------------------------------------------------------------
| Placeholder
|----------------------------------------------------------------------------*/

.jp-Cell-Placeholder {
  padding-left: 55px;
}

.jp-Cell-Placeholder-wrapper {
  background: #fff;
  border: 1px solid;
  border-color: #e5e6e9 #dfe0e4 #d0d1d5;
  border-radius: 4px;
  -webkit-border-radius: 4px;
  margin: 10px 15px;
}

.jp-Cell-Placeholder-wrapper-inner {
  padding: 15px;
  position: relative;
}

.jp-Cell-Placeholder-wrapper-body {
  background-repeat: repeat;
  background-size: 50% auto;
}

.jp-Cell-Placeholder-wrapper-body div {
  background: #f6f7f8;
  background-image: -webkit-linear-gradient(
    left,
    #f6f7f8 0%,
    #edeef1 20%,
    #f6f7f8 40%,
    #f6f7f8 100%
  );
  background-repeat: no-repeat;
  background-size: 800px 104px;
  height: 104px;
  position: absolute;
  right: 15px;
  left: 15px;
  top: 15px;
}

div.jp-Cell-Placeholder-h1 {
  top: 20px;
  height: 20px;
  left: 15px;
  width: 150px;
}

div.jp-Cell-Placeholder-h2 {
  left: 15px;
  top: 50px;
  height: 10px;
  width: 100px;
}

div.jp-Cell-Placeholder-content-1,
div.jp-Cell-Placeholder-content-2,
div.jp-Cell-Placeholder-content-3 {
  left: 15px;
  right: 15px;
  height: 10px;
}

div.jp-Cell-Placeholder-content-1 {
  top: 100px;
}

div.jp-Cell-Placeholder-content-2 {
  top: 120px;
}

div.jp-Cell-Placeholder-content-3 {
  top: 140px;
}

</style>
<style type="text/css">
/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*
The following CSS variables define the main, public API for styling JupyterLab.
These variables should be used by all plugins wherever possible. In other
words, plugins should not define custom colors, sizes, etc unless absolutely
necessary. This enables users to change the visual theme of JupyterLab
by changing these variables.

Many variables appear in an ordered sequence (0,1,2,3). These sequences
are designed to work well together, so for example, `--jp-border-color1` should
be used with `--jp-layout-color1`. The numbers have the following meanings:

* 0: super-primary, reserved for special emphasis
* 1: primary, most important under normal situations
* 2: secondary, next most important under normal situations
* 3: tertiary, next most important under normal situations

Throughout JupyterLab, we are mostly following principles from Google's
Material Design when selecting colors. We are not, however, following
all of MD as it is not optimized for dense, information rich UIs.
*/

:root {
  /* Elevation
   *
   * We style box-shadows using Material Design's idea of elevation. These particular numbers are taken from here:
   *
   * https://github.com/material-components/material-components-web
   * https://material-components-web.appspot.com/elevation.html
   */

  --jp-shadow-base-lightness: 0;
  --jp-shadow-umbra-color: rgba(
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    0.2
  );
  --jp-shadow-penumbra-color: rgba(
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    0.14
  );
  --jp-shadow-ambient-color: rgba(
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    0.12
  );
  --jp-elevation-z0: none;
  --jp-elevation-z1: 0 2px 1px -1px var(--jp-shadow-umbra-color),
    0 1px 1px 0 var(--jp-shadow-penumbra-color),
    0 1px 3px 0 var(--jp-shadow-ambient-color);
  --jp-elevation-z2: 0 3px 1px -2px var(--jp-shadow-umbra-color),
    0 2px 2px 0 var(--jp-shadow-penumbra-color),
    0 1px 5px 0 var(--jp-shadow-ambient-color);
  --jp-elevation-z4: 0 2px 4px -1px var(--jp-shadow-umbra-color),
    0 4px 5px 0 var(--jp-shadow-penumbra-color),
    0 1px 10px 0 var(--jp-shadow-ambient-color);
  --jp-elevation-z6: 0 3px 5px -1px var(--jp-shadow-umbra-color),
    0 6px 10px 0 var(--jp-shadow-penumbra-color),
    0 1px 18px 0 var(--jp-shadow-ambient-color);
  --jp-elevation-z8: 0 5px 5px -3px var(--jp-shadow-umbra-color),
    0 8px 10px 1px var(--jp-shadow-penumbra-color),
    0 3px 14px 2px var(--jp-shadow-ambient-color);
  --jp-elevation-z12: 0 7px 8px -4px var(--jp-shadow-umbra-color),
    0 12px 17px 2px var(--jp-shadow-penumbra-color),
    0 5px 22px 4px var(--jp-shadow-ambient-color);
  --jp-elevation-z16: 0 8px 10px -5px var(--jp-shadow-umbra-color),
    0 16px 24px 2px var(--jp-shadow-penumbra-color),
    0 6px 30px 5px var(--jp-shadow-ambient-color);
  --jp-elevation-z20: 0 10px 13px -6px var(--jp-shadow-umbra-color),
    0 20px 31px 3px var(--jp-shadow-penumbra-color),
    0 8px 38px 7px var(--jp-shadow-ambient-color);
  --jp-elevation-z24: 0 11px 15px -7px var(--jp-shadow-umbra-color),
    0 24px 38px 3px var(--jp-shadow-penumbra-color),
    0 9px 46px 8px var(--jp-shadow-ambient-color);

  /* Borders
   *
   * The following variables, specify the visual styling of borders in JupyterLab.
   */

  --jp-border-width: 1px;
  --jp-border-color0: var(--md-grey-400);
  --jp-border-color1: var(--md-grey-400);
  --jp-border-color2: var(--md-grey-300);
  --jp-border-color3: var(--md-grey-200);
  --jp-inverse-border-color: var(--md-grey-600);
  --jp-border-radius: 2px;

  /* UI Fonts
   *
   * The UI font CSS variables are used for the typography all of the JupyterLab
   * user interface elements that are not directly user generated content.
   *
   * The font sizing here is done assuming that the body font size of --jp-ui-font-size1
   * is applied to a parent element. When children elements, such as headings, are sized
   * in em all things will be computed relative to that body size.
   */

  --jp-ui-font-scale-factor: 1.2;
  --jp-ui-font-size0: 0.83333em;
  --jp-ui-font-size1: 13px; /* Base font size */
  --jp-ui-font-size2: 1.2em;
  --jp-ui-font-size3: 1.44em;
  --jp-ui-font-family: system-ui, -apple-system, blinkmacsystemfont, 'Segoe UI',
    helvetica, arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji',
    'Segoe UI Symbol';

  /*
   * Use these font colors against the corresponding main layout colors.
   * In a light theme, these go from dark to light.
   */

  /* Defaults use Material Design specification */
  --jp-ui-font-color0: rgba(0, 0, 0, 1);
  --jp-ui-font-color1: rgba(0, 0, 0, 0.87);
  --jp-ui-font-color2: rgba(0, 0, 0, 0.54);
  --jp-ui-font-color3: rgba(0, 0, 0, 0.38);

  /*
   * Use these against the brand/accent/warn/error colors.
   * These will typically go from light to darker, in both a dark and light theme.
   */

  --jp-ui-inverse-font-color0: rgba(255, 255, 255, 1);
  --jp-ui-inverse-font-color1: rgba(255, 255, 255, 1);
  --jp-ui-inverse-font-color2: rgba(255, 255, 255, 0.7);
  --jp-ui-inverse-font-color3: rgba(255, 255, 255, 0.5);

  /* Content Fonts
   *
   * Content font variables are used for typography of user generated content.
   *
   * The font sizing here is done assuming that the body font size of --jp-content-font-size1
   * is applied to a parent element. When children elements, such as headings, are sized
   * in em all things will be computed relative to that body size.
   */

  --jp-content-line-height: 1.6;
  --jp-content-font-scale-factor: 1.2;
  --jp-content-font-size0: 0.83333em;
  --jp-content-font-size1: 14px; /* Base font size */
  --jp-content-font-size2: 1.2em;
  --jp-content-font-size3: 1.44em;
  --jp-content-font-size4: 1.728em;
  --jp-content-font-size5: 2.0736em;

  /* This gives a magnification of about 125% in presentation mode over normal. */
  --jp-content-presentation-font-size1: 17px;
  --jp-content-heading-line-height: 1;
  --jp-content-heading-margin-top: 1.2em;
  --jp-content-heading-margin-bottom: 0.8em;
  --jp-content-heading-font-weight: 500;

  /* Defaults use Material Design specification */
  --jp-content-font-color0: rgba(0, 0, 0, 1);
  --jp-content-font-color1: rgba(0, 0, 0, 0.87);
  --jp-content-font-color2: rgba(0, 0, 0, 0.54);
  --jp-content-font-color3: rgba(0, 0, 0, 0.38);
  --jp-content-link-color: var(--md-blue-900);
  --jp-content-font-family: system-ui, -apple-system, blinkmacsystemfont,
    'Segoe UI', helvetica, arial, sans-serif, 'Apple Color Emoji',
    'Segoe UI Emoji', 'Segoe UI Symbol';

  /*
   * Code Fonts
   *
   * Code font variables are used for typography of code and other monospaces content.
   */

  --jp-code-font-size: 13px;
  --jp-code-line-height: 1.3077; /* 17px for 13px base */
  --jp-code-padding: 5px; /* 5px for 13px base, codemirror highlighting needs integer px value */
  --jp-code-font-family-default: menlo, consolas, 'DejaVu Sans Mono', monospace;
  --jp-code-font-family: var(--jp-code-font-family-default);

  /* This gives a magnification of about 125% in presentation mode over normal. */
  --jp-code-presentation-font-size: 16px;

  /* may need to tweak cursor width if you change font size */
  --jp-code-cursor-width0: 1.4px;
  --jp-code-cursor-width1: 2px;
  --jp-code-cursor-width2: 4px;

  /* Layout
   *
   * The following are the main layout colors use in JupyterLab. In a light
   * theme these would go from light to dark.
   */

  --jp-layout-color0: white;
  --jp-layout-color1: white;
  --jp-layout-color2: var(--md-grey-200);
  --jp-layout-color3: var(--md-grey-400);
  --jp-layout-color4: var(--md-grey-600);

  /* Inverse Layout
   *
   * The following are the inverse layout colors use in JupyterLab. In a light
   * theme these would go from dark to light.
   */

  --jp-inverse-layout-color0: #111;
  --jp-inverse-layout-color1: var(--md-grey-900);
  --jp-inverse-layout-color2: var(--md-grey-800);
  --jp-inverse-layout-color3: var(--md-grey-700);
  --jp-inverse-layout-color4: var(--md-grey-600);

  /* Brand/accent */

  --jp-brand-color0: var(--md-blue-900);
  --jp-brand-color1: var(--md-blue-700);
  --jp-brand-color2: var(--md-blue-300);
  --jp-brand-color3: var(--md-blue-100);
  --jp-brand-color4: var(--md-blue-50);
  --jp-accent-color0: var(--md-green-900);
  --jp-accent-color1: var(--md-green-700);
  --jp-accent-color2: var(--md-green-300);
  --jp-accent-color3: var(--md-green-100);

  /* State colors (warn, error, success, info) */

  --jp-warn-color0: var(--md-orange-900);
  --jp-warn-color1: var(--md-orange-700);
  --jp-warn-color2: var(--md-orange-300);
  --jp-warn-color3: var(--md-orange-100);
  --jp-error-color0: var(--md-red-900);
  --jp-error-color1: var(--md-red-700);
  --jp-error-color2: var(--md-red-300);
  --jp-error-color3: var(--md-red-100);
  --jp-success-color0: var(--md-green-900);
  --jp-success-color1: var(--md-green-700);
  --jp-success-color2: var(--md-green-300);
  --jp-success-color3: var(--md-green-100);
  --jp-info-color0: var(--md-cyan-900);
  --jp-info-color1: var(--md-cyan-700);
  --jp-info-color2: var(--md-cyan-300);
  --jp-info-color3: var(--md-cyan-100);

  /* Cell specific styles */

  --jp-cell-padding: 5px;
  --jp-cell-collapser-width: 8px;
  --jp-cell-collapser-min-height: 20px;
  --jp-cell-collapser-not-active-hover-opacity: 0.6;
  --jp-cell-editor-background: var(--md-grey-100);
  --jp-cell-editor-border-color: var(--md-grey-300);
  --jp-cell-editor-box-shadow: inset 0 0 2px var(--md-blue-300);
  --jp-cell-editor-active-background: var(--jp-layout-color0);
  --jp-cell-editor-active-border-color: var(--jp-brand-color1);
  --jp-cell-prompt-width: 64px;
  --jp-cell-prompt-font-family: var(--jp-code-font-family-default);
  --jp-cell-prompt-letter-spacing: 0;
  --jp-cell-prompt-opacity: 1;
  --jp-cell-prompt-not-active-opacity: 0.5;
  --jp-cell-prompt-not-active-font-color: var(--md-grey-700);

  /* A custom blend of MD grey and blue 600
   * See https://meyerweb.com/eric/tools/color-blend/#546E7A:1E88E5:5:hex */
  --jp-cell-inprompt-font-color: #307fc1;

  /* A custom blend of MD grey and orange 600
   * https://meyerweb.com/eric/tools/color-blend/#546E7A:F4511E:5:hex */
  --jp-cell-outprompt-font-color: #bf5b3d;

  /* Notebook specific styles */

  --jp-notebook-padding: 10px;
  --jp-notebook-select-background: var(--jp-layout-color1);
  --jp-notebook-multiselected-color: var(--md-blue-50);

  /* The scroll padding is calculated to fill enough space at the bottom of the
  notebook to show one single-line cell (with appropriate padding) at the top
  when the notebook is scrolled all the way to the bottom. We also subtract one
  pixel so that no scrollbar appears if we have just one single-line cell in the
  notebook. This padding is to enable a 'scroll past end' feature in a notebook.
  */
  --jp-notebook-scroll-padding: calc(
    100% - var(--jp-code-font-size) * var(--jp-code-line-height) -
      var(--jp-code-padding) - var(--jp-cell-padding) - 1px
  );

  /* Rendermime styles */

  --jp-rendermime-error-background: #fdd;
  --jp-rendermime-table-row-background: var(--md-grey-100);
  --jp-rendermime-table-row-hover-background: var(--md-light-blue-50);

  /* Dialog specific styles */

  --jp-dialog-background: rgba(0, 0, 0, 0.25);

  /* Console specific styles */

  --jp-console-padding: 10px;

  /* Toolbar specific styles */

  --jp-toolbar-border-color: var(--jp-border-color1);
  --jp-toolbar-micro-height: 8px;
  --jp-toolbar-background: var(--jp-layout-color1);
  --jp-toolbar-box-shadow: 0 0 2px 0 rgba(0, 0, 0, 0.24);
  --jp-toolbar-header-margin: 4px 4px 0 4px;
  --jp-toolbar-active-background: var(--md-grey-300);

  /* Statusbar specific styles */

  --jp-statusbar-height: 24px;

  /* Input field styles */

  --jp-input-box-shadow: inset 0 0 2px var(--md-blue-300);
  --jp-input-active-background: var(--jp-layout-color1);
  --jp-input-hover-background: var(--jp-layout-color1);
  --jp-input-background: var(--md-grey-100);
  --jp-input-border-color: var(--jp-inverse-border-color);
  --jp-input-active-border-color: var(--jp-brand-color1);
  --jp-input-active-box-shadow-color: rgba(19, 124, 189, 0.3);

  /* General editor styles */

  --jp-editor-selected-background: #d9d9d9;
  --jp-editor-selected-focused-background: #d7d4f0;
  --jp-editor-cursor-color: var(--jp-ui-font-color0);

  /* Code mirror specific styles */

  --jp-mirror-editor-keyword-color: #008000;
  --jp-mirror-editor-atom-color: #88f;
  --jp-mirror-editor-number-color: #080;
  --jp-mirror-editor-def-color: #00f;
  --jp-mirror-editor-variable-color: var(--md-grey-900);
  --jp-mirror-editor-variable-2-color: rgb(0, 54, 109);
  --jp-mirror-editor-variable-3-color: #085;
  --jp-mirror-editor-punctuation-color: #05a;
  --jp-mirror-editor-property-color: #05a;
  --jp-mirror-editor-operator-color: #a2f;
  --jp-mirror-editor-comment-color: #408080;
  --jp-mirror-editor-string-color: #ba2121;
  --jp-mirror-editor-string-2-color: #708;
  --jp-mirror-editor-meta-color: #a2f;
  --jp-mirror-editor-qualifier-color: #555;
  --jp-mirror-editor-builtin-color: #008000;
  --jp-mirror-editor-bracket-color: #997;
  --jp-mirror-editor-tag-color: #170;
  --jp-mirror-editor-attribute-color: #00c;
  --jp-mirror-editor-header-color: blue;
  --jp-mirror-editor-quote-color: #090;
  --jp-mirror-editor-link-color: #00c;
  --jp-mirror-editor-error-color: #f00;
  --jp-mirror-editor-hr-color: #999;

  /*
    RTC user specific colors.
    These colors are used for the cursor, username in the editor,
    and the icon of the user.
  */

  --jp-collaborator-color1: #ffad8e;
  --jp-collaborator-color2: #dac83d;
  --jp-collaborator-color3: #72dd76;
  --jp-collaborator-color4: #00e4d0;
  --jp-collaborator-color5: #45d4ff;
  --jp-collaborator-color6: #e2b1ff;
  --jp-collaborator-color7: #ff9de6;

  /* Vega extension styles */

  --jp-vega-background: white;

  /* Sidebar-related styles */

  --jp-sidebar-min-width: 250px;

  /* Search-related styles */

  --jp-search-toggle-off-opacity: 0.5;
  --jp-search-toggle-hover-opacity: 0.8;
  --jp-search-toggle-on-opacity: 1;
  --jp-search-selected-match-background-color: rgb(245, 200, 0);
  --jp-search-selected-match-color: black;
  --jp-search-unselected-match-background-color: var(
    --jp-inverse-layout-color0
  );
  --jp-search-unselected-match-color: var(--jp-ui-inverse-font-color0);

  /* Icon colors that work well with light or dark backgrounds */
  --jp-icon-contrast-color0: var(--md-purple-600);
  --jp-icon-contrast-color1: var(--md-green-600);
  --jp-icon-contrast-color2: var(--md-pink-600);
  --jp-icon-contrast-color3: var(--md-blue-600);

  /* Button colors */
  --jp-accept-color-normal: var(--md-blue-700);
  --jp-accept-color-hover: var(--md-blue-800);
  --jp-accept-color-active: var(--md-blue-900);
  --jp-warn-color-normal: var(--md-red-700);
  --jp-warn-color-hover: var(--md-red-800);
  --jp-warn-color-active: var(--md-red-900);
  --jp-reject-color-normal: var(--md-grey-600);
  --jp-reject-color-hover: var(--md-grey-700);
  --jp-reject-color-active: var(--md-grey-800);

  /* File or activity icons and switch semantic variables */
  --jp-jupyter-icon-color: #f37626;
  --jp-notebook-icon-color: #f37626;
  --jp-json-icon-color: var(--md-orange-700);
  --jp-console-icon-background-color: var(--md-blue-700);
  --jp-console-icon-color: white;
  --jp-terminal-icon-background-color: var(--md-grey-800);
  --jp-terminal-icon-color: var(--md-grey-200);
  --jp-text-editor-icon-color: var(--md-grey-700);
  --jp-inspector-icon-color: var(--md-grey-700);
  --jp-switch-color: var(--md-grey-400);
  --jp-switch-true-position-color: var(--md-orange-900);
}
</style>
<style type="text/css">
/* Force rendering true colors when outputing to pdf */
* {
  -webkit-print-color-adjust: exact;
}

/* Misc */
a.anchor-link {
  display: none;
}

/* Input area styling */
.jp-InputArea {
  overflow: hidden;
}

.jp-InputArea-editor {
  overflow: hidden;
}

.cm-editor.cm-s-jupyter .highlight pre {
/* weird, but --jp-code-padding defined to be 5px but 4px horizontal padding is hardcoded for pre.cm-line */
  padding: var(--jp-code-padding) 4px;
  margin: 0;

  font-family: inherit;
  font-size: inherit;
  line-height: inherit;
  color: inherit;

}

.jp-OutputArea-output pre {
  line-height: inherit;
  font-family: inherit;
}

.jp-RenderedText pre {
  color: var(--jp-content-font-color1);
  font-size: var(--jp-code-font-size);
}

/* Hiding the collapser by default */
.jp-Collapser {
  display: none;
}

@page {
    margin: 0.5in; /* Margin for each printed piece of paper */
}

@media print {
  .jp-Cell-inputWrapper,
  .jp-Cell-outputWrapper {
    display: block;
  }
}
</style>
<!-- Load mathjax -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.7/latest.js?config=TeX-AMS_CHTML-full,Safe"> </script>
<!-- MathJax configuration -->
<script type="text/x-mathjax-config">
    init_mathjax = function() {
        if (window.MathJax) {
        // MathJax loaded
            MathJax.Hub.Config({
                TeX: {
                    equationNumbers: {
                    autoNumber: "AMS",
                    useLabelIds: true
                    }
                },
                tex2jax: {
                    inlineMath: [ ['$','$'], ["\\(","\\)"] ],
                    displayMath: [ ['$$','$$'], ["\\[","\\]"] ],
                    processEscapes: true,
                    processEnvironments: true
                },
                displayAlign: 'center',
                CommonHTML: {
                    linebreaks: {
                    automatic: true
                    }
                }
            });

            MathJax.Hub.Queue(["Typeset", MathJax.Hub]);
        }
    }
    init_mathjax();
    </script>
<!-- End of mathjax configuration --><script type="module">
  document.addEventListener("DOMContentLoaded", async () => {
    const diagrams = document.querySelectorAll(".jp-Mermaid > pre.mermaid");
    // do not load mermaidjs if not needed
    if (!diagrams.length) {
      return;
    }
    const mermaid = (await import("https://cdnjs.cloudflare.com/ajax/libs/mermaid/10.7.0/mermaid.esm.min.mjs")).default;
    const parser = new DOMParser();

    mermaid.initialize({
      maxTextSize: 100000,
      maxEdges: 100000,
      startOnLoad: false,
      fontFamily: window
        .getComputedStyle(document.body)
        .getPropertyValue("--jp-ui-font-family"),
      theme: document.querySelector("body[data-jp-theme-light='true']")
        ? "default"
        : "dark",
    });

    let _nextMermaidId = 0;

    function makeMermaidImage(svg) {
      const img = document.createElement("img");
      const doc = parser.parseFromString(svg, "image/svg+xml");
      const svgEl = doc.querySelector("svg");
      const { maxWidth } = svgEl?.style || {};
      const firstTitle = doc.querySelector("title");
      const firstDesc = doc.querySelector("desc");

      img.setAttribute("src", `data:image/svg+xml,${encodeURIComponent(svg)}`);
      if (maxWidth) {
        img.width = parseInt(maxWidth);
      }
      if (firstTitle) {
        img.setAttribute("alt", firstTitle.textContent);
      }
      if (firstDesc) {
        const caption = document.createElement("figcaption");
        caption.className = "sr-only";
        caption.textContent = firstDesc.textContent;
        return [img, caption];
      }
      return [img];
    }

    async function makeMermaidError(text) {
      let errorMessage = "";
      try {
        await mermaid.parse(text);
      } catch (err) {
        errorMessage = `${err}`;
      }

      const result = document.createElement("details");
      result.className = 'jp-RenderedMermaid-Details';
      const summary = document.createElement("summary");
      summary.className = 'jp-RenderedMermaid-Summary';
      const pre = document.createElement("pre");
      const code = document.createElement("code");
      code.innerText = text;
      pre.appendChild(code);
      summary.appendChild(pre);
      result.appendChild(summary);

      const warning = document.createElement("pre");
      warning.innerText = errorMessage;
      result.appendChild(warning);
      return [result];
    }

    async function renderOneMarmaid(src) {
      const id = `jp-mermaid-${_nextMermaidId++}`;
      const parent = src.parentNode;
      let raw = src.textContent.trim();
      const el = document.createElement("div");
      el.style.visibility = "hidden";
      document.body.appendChild(el);
      let results = null;
      let output = null;
      try {
        let { svg } = await mermaid.render(id, raw, el);
        svg = cleanMermaidSvg(svg);
        results = makeMermaidImage(svg);
        output = document.createElement("figure");
        results.map(output.appendChild, output);
      } catch (err) {
        parent.classList.add("jp-mod-warning");
        results = await makeMermaidError(raw);
        output = results[0];
      } finally {
        el.remove();
      }
      parent.classList.add("jp-RenderedMermaid");
      parent.appendChild(output);
    }


    /**
     * Post-process to ensure mermaid diagrams contain only valid SVG and XHTML.
     */
    function cleanMermaidSvg(svg) {
      return svg.replace(RE_VOID_ELEMENT, replaceVoidElement);
    }


    /**
     * A regular expression for all void elements, which may include attributes and
     * a slash.
     *
     * @see https://developer.mozilla.org/en-US/docs/Glossary/Void_element
     *
     * Of these, only `<br>` is generated by Mermaid in place of `\n`,
     * but _any_ "malformed" tag will break the SVG rendering entirely.
     */
    const RE_VOID_ELEMENT =
      /<\s*(area|base|br|col|embed|hr|img|input|link|meta|param|source|track|wbr)\s*([^>]*?)\s*>/gi;

    /**
     * Ensure a void element is closed with a slash, preserving any attributes.
     */
    function replaceVoidElement(match, tag, rest) {
      rest = rest.trim();
      if (!rest.endsWith('/')) {
        rest = `${rest} /`;
      }
      return `<${tag} ${rest}>`;
    }

    void Promise.all([...diagrams].map(renderOneMarmaid));
  });
</script>
<style>
  .jp-Mermaid:not(.jp-RenderedMermaid) {
    display: none;
  }

  .jp-RenderedMermaid {
    overflow: auto;
    display: flex;
  }

  .jp-RenderedMermaid.jp-mod-warning {
    width: auto;
    padding: 0.5em;
    margin-top: 0.5em;
    border: var(--jp-border-width) solid var(--jp-warn-color2);
    border-radius: var(--jp-border-radius);
    color: var(--jp-ui-font-color1);
    font-size: var(--jp-ui-font-size1);
    white-space: pre-wrap;
    word-wrap: break-word;
  }

  .jp-RenderedMermaid figure {
    margin: 0;
    overflow: auto;
    max-width: 100%;
  }

  .jp-RenderedMermaid img {
    max-width: 100%;
  }

  .jp-RenderedMermaid-Details > pre {
    margin-top: 1em;
  }

  .jp-RenderedMermaid-Summary {
    color: var(--jp-warn-color2);
  }

  .jp-RenderedMermaid:not(.jp-mod-warning) pre {
    display: none;
  }

  .jp-RenderedMermaid-Summary > pre {
    display: inline-block;
    white-space: normal;
  }
</style>
<!-- End of mermaid configuration --></head>
<body class="" data-jp-theme-light="true" data-jp-theme-name="JupyterLab Light">
<main>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">

<p>I will use numpy and a list of functions to build a Deep Neural Network, and apply it to cat vs non-cat classification. More accuracy is expected relative to previous logistic regression implementations. <strong>I will build and apply a deep neural network to supervised learning.</strong></p>

<h3 id="Abstract">Abstract<a class="anchor-link" href="#Abstract">¶</a></h3><p>Deep learning, a subset of machine learning and artificial intelligence, is a learning algorithm that mimic how human brain (neurological system) works. It can recognize complex patterns like image, text and sound.</p>
<p>As an analogy, in neurological system, a neuron receives input from other neurons or external sources, processes these inputs, and generates an output. In the context of deep learning, a neuron can be seen as a function that takes inputs, weights and bias, to compute linear function ($Z^{[l]}=W^{[l]}A^{[l-1]}+b^{[l]}$) and applies activation function ($g(Z^{[l]})$).</p>
<h3 id="Deep-learning-vs.-Machine-learning">Deep learning vs. Machine learning<a class="anchor-link" href="#Deep-learning-vs.-Machine-learning">¶</a></h3><blockquote>
<p>Deep learning eliminates some of data pre-processing that is typically involved with machine learning. These algorithms can ingest and process unstructured data, like text and images, and it automates feature extraction, removing some of the dependency on human experts. For example, let’s say that we had a set of photos of different pets, and we wanted to categorize by “cat”, “dog”, “hamster”, et cetera. Deep learning algorithms can determine which features (e.g. ears) are most important to distinguish each animal from another. In machine learning, this hierarchy of features is established manually by a human expert.</p>
</blockquote>
<blockquote>
<p>Then, through the processes of gradient descent and backpropagation, the deep learning algorithm adjusts and fits itself for accuracy, allowing it to make predictions about a new photo of an animal with increased precision.</p>
</blockquote>
<blockquote>
<p>Source: <a href="https://www.ibm.com/topics/deep-learning">https://www.ibm.com/topics/deep-learning</a></p>
</blockquote>
<h3 id="Forward-and-Backward-Propagation">Forward and Backward Propagation<a class="anchor-link" href="#Forward-and-Backward-Propagation">¶</a></h3><p>Forward propagation involves passing input data through a neural network to obtain predictions.
Backward propagation computes gradients of model parameters with respect to a loss function.
By adjusting weights based on gradients, the model gradually improves its predictions.</p>
<ul>
<li><strong>Forward propagation</strong>   $A^{[l-1]}, W^{[l]}, b^{[l]} \rightarrow Z^{[l]}, A^{[l]}$</li>
</ul>
<p>$$Z^{[l]} = W^{[l]} A^{[l-1]} + b^{[l]}$$</p>
<p>$$A^{[l]} = g^{[l]} (Z^{[l]})$$</p>
<ul>
<li><strong>Backward propagation</strong>   $dA^{[l]} \rightarrow dA^{[l-1]},dW^{[l]}, db^{[l]}$</li>
</ul>
<p>$$dZ^{[l]} = dA^{[l]} * {g^{[l]}}^{'}(Z^{[l]})$$</p>
<p>$$dW^{[l]} = \frac{1}{m}dZ^{[l]}{A^{[l-1]}}^T$$</p>
<p>$$db^{[l]} = \frac{1}{m}np.sum(dZ^{[l]}, axis=1, keepdims=True)$$</p>
<p>$$dA^{[l-1]} = {W^{[l]}}^T dZ^{[l]} = \frac{dJ}{dA^{[l-1]}} = \frac{dZ^{[l]}}{dA^{[l-1]}} \frac{dJ}{dZ^{[l]}} = \frac{dZ^{[l]}}{dA^{[l-1]}} dZ^{[l]}$$</p>
<p>$$, where \hspace{3mm} dZ^{[L]} = A^{[L]}-Y$$</p>
<p>Also, we have a Loss function $L = -YlogA -(1-Y)log(1-A)$</p>
<img alt="No description has been provided for this image" src="https://imgur.com/IzQKi3g.png" style="width:650px;height:400px;"/>
<caption><center> <u>Figure 2</u>: 2-layer neural network. <br/> The model can be summarized as: ***INPUT -&gt; LINEAR -&gt; RELU -&gt; LINEAR -&gt; SIGMOID -&gt; OUTPUT***. </center></caption>
<img alt="No description has been provided for this image" src="https://imgur.com/XPElFUZ.png" style="width:650px;height:400px;"/>
<caption><center> <u>Figure 3</u>: L-layer neural network. <br/> The model can be summarized as: ***[LINEAR -&gt; RELU] $\times$ (L-1) -&gt; LINEAR -&gt; SIGMOID***</center></caption>
<h3 id="Objective">Objective<a class="anchor-link" href="#Objective">¶</a></h3><p>In the following Jupyter notebook, I go through what I've learned from Andrew Ng's deep learning specialization course.</p>
<p>I revisit the model for training L-layer deep neural network that can identify cats as binary ouput of 0(non-cat) and 1(cat). The training and test data are provided from the lecture. Here are the list of methods that I'm going to implement:</p>
<div class="highlight"><pre><span></span><span class="c1"># 1. initialize</span>
<span class="k">def</span> <span class="nf">initialize_parameters_deep</span><span class="p">(</span><span class="n">layer_dims</span><span class="p">):</span>
  <span class="k">return</span> <span class="n">parameters</span>

<span class="c1"># 2. linear forward</span>
<span class="k">def</span> <span class="nf">relu</span><span class="p">(</span><span class="n">Z</span><span class="p">):</span>
  <span class="k">return</span> <span class="n">A</span><span class="p">,</span> <span class="n">cache</span>

<span class="k">def</span> <span class="nf">sigmoid</span><span class="p">(</span><span class="n">Z</span><span class="p">):</span>
  <span class="k">return</span> <span class="n">A</span><span class="p">,</span> <span class="n">cache</span>

<span class="k">def</span> <span class="nf">linear_forward</span><span class="p">(</span><span class="n">A</span><span class="p">,</span> <span class="n">W</span><span class="p">,</span> <span class="n">b</span><span class="p">):</span>
  <span class="k">return</span> <span class="n">Z</span><span class="p">,</span> <span class="n">cache</span>

<span class="c1"># 3. activation forward</span>
<span class="k">def</span> <span class="nf">linear_activation_forward</span><span class="p">(</span><span class="n">A_prev</span><span class="p">,</span> <span class="n">W</span><span class="p">,</span> <span class="n">b</span><span class="p">,</span> <span class="n">activation</span><span class="p">):</span>
  <span class="k">return</span> <span class="n">A</span><span class="p">,</span> <span class="n">cache</span>

<span class="c1"># 4. nn forward</span>
<span class="k">def</span> <span class="nf">L_model_forward</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="n">parameters</span><span class="p">):</span>
  <span class="k">return</span> <span class="n">AL</span><span class="p">,</span> <span class="n">caches</span>

<span class="c1"># 5. compute cost</span>
<span class="k">def</span> <span class="nf">compute_cost</span><span class="p">(</span><span class="n">AL</span><span class="p">,</span> <span class="n">Y</span><span class="p">):</span>
  <span class="k">return</span> <span class="n">cost</span>

<span class="c1"># 6. backward propagation</span>
<span class="c1"># dZ = dA * g'(Z) where g(Z) = relu</span>
<span class="k">def</span> <span class="nf">relu_backward</span><span class="p">(</span><span class="n">dA</span><span class="p">,</span> <span class="n">cache</span><span class="p">):</span>
  <span class="k">return</span> <span class="n">dZ</span>

<span class="c1"># dZ = dA * g'(Z) where g(Z) = sigmoid,</span>
<span class="c1"># g'(Z) = g(Z)(1- g(Z))</span>
<span class="k">def</span> <span class="nf">sigmoid_backward</span><span class="p">(</span><span class="n">dA</span><span class="p">,</span> <span class="n">cache</span><span class="p">):</span>
  <span class="k">return</span> <span class="n">dZ</span>

<span class="k">def</span> <span class="nf">linear_backward</span><span class="p">(</span><span class="n">dZ</span><span class="p">,</span> <span class="n">linear_cache</span><span class="p">):</span>
  <span class="k">return</span> <span class="n">dA_prev</span><span class="p">,</span> <span class="n">dW</span><span class="p">,</span> <span class="n">db</span>

<span class="k">def</span> <span class="nf">linear_activation_backward</span><span class="p">(</span><span class="n">dA</span><span class="p">,</span> <span class="n">cache</span><span class="p">,</span> <span class="n">activation</span><span class="p">):</span>
  <span class="k">return</span> <span class="n">dA_prev</span><span class="p">,</span> <span class="n">dW</span><span class="p">,</span> <span class="n">db</span>

<span class="k">def</span> <span class="nf">compute_dA</span><span class="p">(</span><span class="n">A</span><span class="p">,</span><span class="n">Y</span><span class="p">):</span>
  <span class="k">return</span> <span class="n">dA</span>

<span class="k">def</span> <span class="nf">L_model_backward</span><span class="p">(</span><span class="n">AL</span><span class="p">,</span> <span class="n">Y</span><span class="p">,</span> <span class="n">caches</span><span class="p">):</span>
  <span class="k">return</span> <span class="n">grads</span>

<span class="c1"># 7. update parameters</span>
<span class="k">def</span> <span class="nf">update_parameters</span><span class="p">(</span><span class="n">parameters</span><span class="p">,</span> <span class="n">grads</span><span class="p">,</span> <span class="n">learning_rate</span><span class="p">):</span>
  <span class="k">return</span> <span class="n">parameters</span>

<span class="c1"># 8. predict</span>
<span class="k">def</span> <span class="nf">predict</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> <span class="n">parameters</span><span class="p">):</span>
  <span class="k">return</span> <span class="n">np</span><span class="o">.</span><span class="n">zeros</span><span class="p">((</span><span class="mi">1</span><span class="p">,</span><span class="n">m</span><span class="p">))</span>
</pre></div>
<h3 id="Related-Topics">Related Topics<a class="anchor-link" href="#Related-Topics">¶</a></h3><ul>
<li><a href="https://www.youtube.com/watch?v=iHCeAotHZa4">Geoffrey Hinton: Will digital intelligence replace biological intelligence?</a></li>
<li><a href="https://www.youtube.com/watch?v=2IK3DFHRFfw">Henrik Kniberg: Generative AI in a Nutshell</a></li>
<li><a href="https://www.youtube.com/watch?v=0QczhVg5HaI">Emergent Garden: Why Neural Networks can learn (almost) anything</a></li>
<li><a href="https://www.youtube.com/watch?v=TkwXa7Cvfr8">Emergent Garden: Watching Neural Networks Learn</a></li>
<li><a href="https://www.youtube.com/watch?v=JoFW2uSd3Uo">Steve Brunton: Physics Informed Machine Learning</a></li>
<li><a href="https://blog.gregbrockman.com/how-i-became-a-machine-learning-practitioner">How I became a machine learning practitioner</a></li>
<li><a href="https://podcasts.apple.com/tw/podcast/gavin-uberti-real-time-ai-the-future-of-ai-hardware/id1154105909?i=1000638288111">Gavin Uberti - Real-Time AI &amp; The Future of AI Hardware</a></li>
<li><a href="https://www.youtube.com/watch?v=z1rHPFiY6FA">Michael Royzen: Beating GPT-4 with Open Source Models (Phind)</a></li>
<li><a href="https://www.youtube.com/watch?v=fmI_OciHV_8">YC Combinator AI startup by college kids (2024)</a></li>
<li><a href="https://www.youtube.com/watch?v=UTuuTTnjxMQ">Sholto Douglas &amp; Trenton Bricken - How to Build &amp; Understand GPT-7's Mind</a></li>
</ul>
<h2 id="Reference">Reference<a class="anchor-link" href="#Reference">¶</a></h2><ul>
<li><a href="https://www.amazon.com/Make-Your-Own-Neural-Network/dp/1530826608">Make Your Own Neural Network</a></li>
<li><a href="https://nnfs.io/">Neural Networks From Scratch</a></li>
<li><a href="https://udlbook.github.io/udlbook/">Understanding Deep Learning</a></li>
<li><a href="https://bishopbook.com/">Deep Learning: Foundations and Concepts</a></li>
<li><a href="https://www.learnpytorch.io/">Zero to Mastery Learn PyTorch for Deep Learning</a></li>
<li><a href="https://github.com/rasbt/LLMs-from-scratch">LLMs from scratch</a></li>
<li><a href="https://www.youtube.com/watch?v=VMj-3S1tku0">Andrej Karpathy, intro to neural networks and backpropagation: building micrograd</a></li>
<li><a href="https://www.chenyang.co/diffusion.html">Diffusion models from scratch, from a new theoretical perspective</a></li>
<li><a href="https://www.youtube.com/watch?v=aircAruvnKk">3Blue1Brown: But what is a neural network?</a></li>
<li><a href="https://www.youtube.com/watch?v=eMlx5fFNoYc">3Blue1Brown: Visualizing Attention, a Transformer's Heart</a></li>
<li><a href="https://thegradient.pub/mamba-explained/">Mamba explained</a></li>
<li><a href="https://justine.lol/matmul/">LLaMA Now Goes Faster on CPUs</a></li>
<li><a href="https://www.youtube.com/watch?v=Bg1LQ_jWliU">Mamba-Palooza: 90 Days of Mamba-Inspired Research with Jason Meaux: Part 1</a></li>
<li><a href="https://www.youtube.com/watch?v=MwIiQsEVyew">Mamba-Palooza: 90 Days of Mamba-Inspired Research with Jason Meaux: Part 2</a></li>
</ul>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>Let's first import all the packages that you will need during this assignment.</p>
<ul>
<li><a href="www.numpy.org">numpy</a> is the fundamental package for scientific computing with Python.</li>
<li><a href="http://matplotlib.org">matplotlib</a> is a library to plot graphs in Python.</li>
<li><a href="http://www.h5py.org">h5py</a> is a common package to interact with a dataset that is stored on an H5 file.</li>
<li><a href="http://www.pythonware.com/products/pil/">PIL</a> and <a href="https://www.scipy.org/">scipy</a> are used here to test your model with your own picture at the end.</li>
<li>dnn_app_utils provides the functions implemented in the "Building your Deep Neural Network: Step by Step" assignment to this notebook.</li>
<li>np.random.seed(1) is used to keep all the random function calls consistent. It will help us grade your work.</li>
</ul>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="1---Packages">1 - Packages<a class="anchor-link" href="#1---Packages">¶</a></h2>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [ ]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="kn">import</span> <span class="nn">time</span>
<span class="kn">import</span> <span class="nn">numpy</span> <span class="k">as</span> <span class="nn">np</span>
<span class="kn">import</span> <span class="nn">h5py</span>
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="k">as</span> <span class="nn">plt</span>
<span class="kn">import</span> <span class="nn">scipy</span>
<span class="kn">from</span> <span class="nn">PIL</span> <span class="kn">import</span> <span class="n">Image</span>
<span class="kn">from</span> <span class="nn">scipy</span> <span class="kn">import</span> <span class="n">ndimage</span>
<span class="kn">from</span> <span class="nn">dnn_app_utils_v3</span> <span class="kn">import</span> <span class="o">*</span>

<span class="o">%</span><span class="k">matplotlib</span> inline
<span class="n">plt</span><span class="o">.</span><span class="n">rcParams</span><span class="p">[</span><span class="s1">'figure.figsize'</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="mf">5.0</span><span class="p">,</span> <span class="mf">4.0</span><span class="p">)</span> <span class="c1"># set default size of plots</span>
<span class="n">plt</span><span class="o">.</span><span class="n">rcParams</span><span class="p">[</span><span class="s1">'image.interpolation'</span><span class="p">]</span> <span class="o">=</span> <span class="s1">'nearest'</span>
<span class="n">plt</span><span class="o">.</span><span class="n">rcParams</span><span class="p">[</span><span class="s1">'image.cmap'</span><span class="p">]</span> <span class="o">=</span> <span class="s1">'gray'</span>

<span class="o">%</span><span class="k">load_ext</span> autoreload
<span class="o">%</span><span class="k">autoreload</span> 2

<span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">seed</span><span class="p">(</span><span class="mi">1</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="2---Dataset">2 - Dataset<a class="anchor-link" href="#2---Dataset">¶</a></h2><p>You will use the same "Cat vs non-Cat" dataset as in "Logistic Regression as a Neural Network" (Assignment 2). The model you had built had 70% test accuracy on classifying cats vs non-cats images. Hopefully, your new model will perform a better!</p>
<p><strong>Problem Statement</strong>: You are given a dataset ("data.h5") containing:
- a training set of m_train images labelled as cat (1) or non-cat (0)
- a test set of m_test images labelled as cat and non-cat
- each image is of shape (num_px, num_px, 3) where 3 is for the 3 channels (RGB).</p>
<p>Let's get more familiar with the dataset. Load the data by running the cell below.</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [ ]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">train_x_orig</span><span class="p">,</span> <span class="n">train_y</span><span class="p">,</span> <span class="n">test_x_orig</span><span class="p">,</span> <span class="n">test_y</span><span class="p">,</span> <span class="n">classes</span> <span class="o">=</span> <span class="n">load_data</span><span class="p">()</span>
<span class="c1"># m = 209</span>
<span class="nb">print</span><span class="p">(</span><span class="n">train_x_orig</span><span class="o">.</span><span class="n">shape</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">train_y</span><span class="o">.</span><span class="n">shape</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>(209, 64, 64, 3)
(1, 209)
</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>The following code will show you an image in the dataset. Feel free to change the index and re-run the cell multiple times to see other images.</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [ ]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1"># Example of a picture</span>
<span class="n">index</span> <span class="o">=</span> <span class="mi">10</span>
<span class="n">plt</span><span class="o">.</span><span class="n">imshow</span><span class="p">(</span><span class="n">test_x_orig</span><span class="p">[</span><span class="n">index</span><span class="p">])</span>
<span class="nb">print</span> <span class="p">(</span><span class="s2">"y = "</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">test_y</span><span class="p">[</span><span class="mi">0</span><span class="p">,</span><span class="n">index</span><span class="p">])</span> <span class="o">+</span> <span class="s2">". It's a "</span> <span class="o">+</span> <span class="n">classes</span><span class="p">[</span><span class="n">test_y</span><span class="p">[</span><span class="mi">0</span><span class="p">,</span><span class="n">index</span><span class="p">]]</span><span class="o">.</span><span class="n">decode</span><span class="p">(</span><span class="s2">"utf-8"</span><span class="p">)</span> <span class="o">+</span>  <span class="s2">" picture."</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>y = 1. It's a cat picture.
</pre>
</div>
</div>
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedImage jp-OutputArea-output" tabindex="0">
<img alt="No description has been provided for this image" class="" src="data:image/png;base64,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vHkATuEzPGVS4BSyceNGL5VKeQ899JC3fft27xOf+ITX2Njo9fT0TPfUKIODg96LL77ovfjiix4A7xvf+Ib34osveq+//rrneZ53zz33eI2Njd4Pf/hD7ze/+Y13/fXXe/Pnz/dGR0eneeaed+utt3rZbNZ75plnvP3794/9jIyMjPX55Cc/6c2dO9f72c9+5r3wwgteZ2en19nZOY2zfpPPfe5z3ubNm73du3d7v/nNb7zPfe5zXiQS8f7zP//T87xwz/14HPs2heeF/xg+/elPe88884y3e/du79lnn/W6urq8GTNmeH19fZ7nhX/+zz//vBePx72vfOUr3s6dO71/+Zd/8Wpqarx//ud/HutzKp7hUC7Gnud53/rWt7y5c+d6yWTSu/zyy72tW7dO95SOy89//nMPR8vC+n5WrFjhed7RV2O+8IUveK2trV4qlfKuueYab8eOHdM76T/A5g3A27Bhw1if0dFR72/+5m+8pqYmr6amxvuLv/gLb//+/dM36WP4+Mc/7s2bN89LJpPezJkzvWuuuWZsIfa8cM/9eLiLcdiP4aabbvLa29u9ZDLpnXXWWd5NN93k7dq1a+z3YZ+/53nej3/8Y+/CCy/0UqmUt3DhQu+73/2u7/en4hlWPmMhhAgBoYsZCyHE2xEtxkIIEQK0GAshRAjQYiyEECFAi7EQQoQALcZCCBECtBgLIUQI0GIshBAhQIuxEEKEAC3GQggRArQYCyFECPj/yDmVFX3hHwwAAAAASUVORK5CYII="/>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [ ]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="nb">print</span><span class="p">(</span><span class="n">train_x_orig</span><span class="o">.</span><span class="n">shape</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">test_x_orig</span><span class="o">.</span><span class="n">shape</span><span class="p">)</span>

<span class="c1"># Explore your dataset </span>
<span class="n">m_train</span> <span class="o">=</span> <span class="n">train_x_orig</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span>
<span class="n">num_px</span> <span class="o">=</span> <span class="n">train_x_orig</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">1</span><span class="p">]</span>
<span class="n">m_test</span> <span class="o">=</span> <span class="n">test_x_orig</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span>

<span class="nb">print</span> <span class="p">(</span><span class="s2">"Number of training examples: "</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">m_train</span><span class="p">))</span>
<span class="nb">print</span> <span class="p">(</span><span class="s2">"Number of testing examples: "</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">m_test</span><span class="p">))</span>
<span class="nb">print</span> <span class="p">(</span><span class="s2">"Each image is of size: ("</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">num_px</span><span class="p">)</span> <span class="o">+</span> <span class="s2">", "</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">num_px</span><span class="p">)</span> <span class="o">+</span> <span class="s2">", 3)"</span><span class="p">)</span>
<span class="nb">print</span> <span class="p">(</span><span class="s2">"train_x_orig shape: "</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">train_x_orig</span><span class="o">.</span><span class="n">shape</span><span class="p">))</span>
<span class="nb">print</span> <span class="p">(</span><span class="s2">"train_y shape: "</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">train_y</span><span class="o">.</span><span class="n">shape</span><span class="p">))</span>
<span class="nb">print</span> <span class="p">(</span><span class="s2">"test_x_orig shape: "</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">test_x_orig</span><span class="o">.</span><span class="n">shape</span><span class="p">))</span>
<span class="nb">print</span> <span class="p">(</span><span class="s2">"test_y shape: "</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">test_y</span><span class="o">.</span><span class="n">shape</span><span class="p">))</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>(209, 64, 64, 3)
(50, 64, 64, 3)
Number of training examples: 209
Number of testing examples: 50
Each image is of size: (64, 64, 3)
train_x_orig shape: (209, 64, 64, 3)
train_y shape: (1, 209)
test_x_orig shape: (50, 64, 64, 3)
test_y shape: (1, 50)
</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>As usual, you reshape and standardize the images before feeding them to the network. The code is given in the cell below.</p>
<img alt="No description has been provided for this image" src="images/imvectorkiank.png" style="width:450px;height:300px;"/>
<caption><center> <u>Figure 1</u>: Image to vector conversion. <br/> </center></caption>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [ ]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1"># Reshape the training and test examples </span>
<span class="n">train_x_flatten</span> <span class="o">=</span> <span class="n">train_x_orig</span><span class="o">.</span><span class="n">reshape</span><span class="p">(</span><span class="n">train_x_orig</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">],</span> <span class="o">-</span><span class="mi">1</span><span class="p">)</span><span class="o">.</span><span class="n">T</span>   <span class="c1"># The "-1" makes reshape flatten the remaining dimensions</span>
<span class="n">test_x_flatten</span> <span class="o">=</span> <span class="n">test_x_orig</span><span class="o">.</span><span class="n">reshape</span><span class="p">(</span><span class="n">test_x_orig</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">],</span> <span class="o">-</span><span class="mi">1</span><span class="p">)</span><span class="o">.</span><span class="n">T</span>

<span class="c1"># Standardize data to have feature values between 0 and 1.</span>
<span class="n">train_x</span> <span class="o">=</span> <span class="n">train_x_flatten</span><span class="o">/</span><span class="mf">255.</span>
<span class="n">test_x</span> <span class="o">=</span> <span class="n">test_x_flatten</span><span class="o">/</span><span class="mf">255.</span>

<span class="nb">print</span> <span class="p">(</span><span class="s2">"train_x's shape: "</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">train_x</span><span class="o">.</span><span class="n">shape</span><span class="p">))</span>
<span class="nb">print</span> <span class="p">(</span><span class="s2">"test_x's shape: "</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">test_x</span><span class="o">.</span><span class="n">shape</span><span class="p">))</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>train_x's shape: (12288, 209)
test_x's shape: (12288, 50)
</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>$12,288$ equals $64 \times 64 \times 3$ which is the size of one reshaped image vector.</p>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="3---Architecture-of-your-model">3 - Architecture of your model<a class="anchor-link" href="#3---Architecture-of-your-model">¶</a></h2>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>Now that you are familiar with the dataset, it is time to build a deep neural network to distinguish cat images from non-cat images.</p>
<p>You will build two different models:</p>
<ul>
<li>A 2-layer neural network</li>
<li>An L-layer deep neural network</li>
</ul>
<p>You will then compare the performance of these models, and also try out different values for $L$.</p>
<p>Let's look at the two architectures.</p>
<h3 id="3.1---2-layer-neural-network">3.1 - 2-layer neural network<a class="anchor-link" href="#3.1---2-layer-neural-network">¶</a></h3><img alt="No description has been provided for this image" src="https://imgur.com/IzQKi3g.png" style="width:650px;height:400px;"/>
<caption><center> <u>Figure 2</u>: 2-layer neural network. <br/> The model can be summarized as: ***INPUT -&gt; LINEAR -&gt; RELU -&gt; LINEAR -&gt; SIGMOID -&gt; OUTPUT***. </center></caption>
<p><u>Detailed Architecture of figure 2</u>:</p>
<ul>
<li>The input is a (64,64,3) image which is flattened to a vector of size $(12288,1)$.</li>
<li>The corresponding vector: $[x_0,x_1,...,x_{12287}]^T$ is then multiplied by the weight matrix $W^{[1]}$ of size $(n^{[1]}, 12288)$.</li>
<li>You then add a bias term and take its relu to get the following vector: $[a_0^{[1]}, a_1^{[1]},..., a_{n^{[1]}-1}^{[1]}]^T$.</li>
<li>You then repeat the same process.</li>
<li>You multiply the resulting vector by $W^{[2]}$ and add your intercept (bias).</li>
<li>Finally, you take the sigmoid of the result. If it is greater than 0.5, you classify it to be a cat.</li>
</ul>
<h3 id="3.2---L-layer-deep-neural-network">3.2 - L-layer deep neural network<a class="anchor-link" href="#3.2---L-layer-deep-neural-network">¶</a></h3><p>It is hard to represent an L-layer deep neural network with the above representation. However, here is a simplified network representation:</p>
<img alt="No description has been provided for this image" src="https://imgur.com/XPElFUZ.png" style="width:650px;height:400px;"/>
<caption><center> <u>Figure 3</u>: L-layer neural network. <br/> The model can be summarized as: ***[LINEAR -&gt; RELU] $\times$ (L-1) -&gt; LINEAR -&gt; SIGMOID***</center></caption>
<p><u>Detailed Architecture of figure 3</u>:</p>
<ul>
<li>The input is a (64,64,3) image which is flattened to a vector of size (12288,1).</li>
<li>The corresponding vector: $[x_0,x_1,...,x_{12287}]^T$ is then multiplied by the weight matrix $W^{[1]}$ and then you add the intercept $b^{[1]}$. The result is called the linear unit.</li>
<li>Next, you take the relu of the linear unit. This process could be repeated several times for each $(W^{[l]}, b^{[l]})$ depending on the model architecture.</li>
<li>Finally, you take the sigmoid of the final linear unit. If it is greater than 0.5, you classify it to be a cat.</li>
</ul>
<h3 id="3.3---General-methodology">3.3 - General methodology<a class="anchor-link" href="#3.3---General-methodology">¶</a></h3><p>As usual you will follow the Deep Learning methodology to build the model:
1. Initialize parameters / Define hyperparameters
2. Loop for num_iterations:
a. Forward propagation
b. Compute cost function
c. Backward propagation
d. Update parameters (using parameters, and grads from backprop)
4. Use trained parameters to predict labels</p>
<p>Let's now implement those two models!</p>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="4---Two-layer-neural-network">4 - Two-layer neural network<a class="anchor-link" href="#4---Two-layer-neural-network">¶</a></h2><p><strong>Question</strong>:  Use the helper functions you have implemented in the previous assignment to build a 2-layer neural network with the following structure: <em>LINEAR -&gt; RELU -&gt; LINEAR -&gt; SIGMOID</em>. The functions you may need and their inputs are:</p>
<div class="highlight"><pre><span></span><span class="k">def</span> <span class="nf">initialize_parameters</span><span class="p">(</span><span class="n">n_x</span><span class="p">,</span> <span class="n">n_h</span><span class="p">,</span> <span class="n">n_y</span><span class="p">):</span>
    <span class="o">...</span>
    <span class="k">return</span> <span class="n">parameters</span> 
<span class="k">def</span> <span class="nf">linear_activation_forward</span><span class="p">(</span><span class="n">A_prev</span><span class="p">,</span> <span class="n">W</span><span class="p">,</span> <span class="n">b</span><span class="p">,</span> <span class="n">activation</span><span class="p">):</span>
    <span class="o">...</span>
    <span class="k">return</span> <span class="n">A</span><span class="p">,</span> <span class="n">cache</span>
<span class="k">def</span> <span class="nf">compute_cost</span><span class="p">(</span><span class="n">AL</span><span class="p">,</span> <span class="n">Y</span><span class="p">):</span>
    <span class="o">...</span>
    <span class="k">return</span> <span class="n">cost</span>
<span class="k">def</span> <span class="nf">linear_activation_backward</span><span class="p">(</span><span class="n">dA</span><span class="p">,</span> <span class="n">cache</span><span class="p">,</span> <span class="n">activation</span><span class="p">):</span>
    <span class="o">...</span>
    <span class="k">return</span> <span class="n">dA_prev</span><span class="p">,</span> <span class="n">dW</span><span class="p">,</span> <span class="n">db</span>
<span class="k">def</span> <span class="nf">update_parameters</span><span class="p">(</span><span class="n">parameters</span><span class="p">,</span> <span class="n">grads</span><span class="p">,</span> <span class="n">learning_rate</span><span class="p">):</span>
    <span class="o">...</span>
    <span class="k">return</span> <span class="n">parameters</span>
</pre></div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [ ]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">### CONSTANTS DEFINING THE MODEL ####</span>
<span class="n">n_x</span> <span class="o">=</span> <span class="mi">12288</span>     <span class="c1"># num_px * num_px * 3</span>
<span class="n">n_h</span> <span class="o">=</span> <span class="mi">7</span>
<span class="n">n_y</span> <span class="o">=</span> <span class="mi">1</span>
<span class="n">layers_dims</span> <span class="o">=</span> <span class="p">(</span><span class="n">n_x</span><span class="p">,</span> <span class="n">n_h</span><span class="p">,</span> <span class="n">n_y</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [ ]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1"># GRADED FUNCTION: two_layer_model</span>

<span class="k">def</span> <span class="nf">two_layer_model</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="n">Y</span><span class="p">,</span> <span class="n">layers_dims</span><span class="p">,</span> <span class="n">learning_rate</span> <span class="o">=</span> <span class="mf">0.0075</span><span class="p">,</span> <span class="n">num_iterations</span> <span class="o">=</span> <span class="mi">3000</span><span class="p">,</span> <span class="n">print_cost</span><span class="o">=</span><span class="kc">False</span><span class="p">):</span>
<span class="w">    </span><span class="sd">"""</span>
<span class="sd">    Implements a  two-layer neural network: LINEAR-&gt;RELU-&gt;LINEAR-&gt;SIGMOID.</span>
<span class="sd">    </span>
<span class="sd">    Arguments:</span>
<span class="sd">    X -- input data, of shape (n_x, number of examples)</span>
<span class="sd">    Y -- true "label" vector (containing 0 if cat, 1 if non-cat), of shape (1, number of examples)</span>
<span class="sd">    layers_dims -- dimensions of the layers (n_x, n_h, n_y)</span>
<span class="sd">    num_iterations -- number of iterations of the optimization loop</span>
<span class="sd">    learning_rate -- learning rate of the gradient descent update rule</span>
<span class="sd">    print_cost -- If set to True, this will print the cost every 100 iterations </span>
<span class="sd">    </span>
<span class="sd">    Returns:</span>
<span class="sd">    parameters -- a dictionary containing W1, W2, b1, and b2</span>
<span class="sd">    """</span>
    
    <span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">seed</span><span class="p">(</span><span class="mi">1</span><span class="p">)</span>
    <span class="n">grads</span> <span class="o">=</span> <span class="p">{}</span>
    <span class="n">costs</span> <span class="o">=</span> <span class="p">[]</span>                              <span class="c1"># to keep track of the cost</span>
    <span class="n">m</span> <span class="o">=</span> <span class="n">X</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">1</span><span class="p">]</span>                           <span class="c1"># number of examples</span>
    <span class="p">(</span><span class="n">n_x</span><span class="p">,</span> <span class="n">n_h</span><span class="p">,</span> <span class="n">n_y</span><span class="p">)</span> <span class="o">=</span> <span class="n">layers_dims</span>
    
    <span class="c1"># Initialize parameters dictionary, by calling one of the functions you'd previously implemented</span>
    <span class="c1">### START CODE HERE ### (≈ 1 line of code)</span>
    <span class="n">parameters</span> <span class="o">=</span> <span class="n">initialize_parameters</span><span class="p">(</span><span class="n">n_x</span><span class="p">,</span> <span class="n">n_h</span><span class="p">,</span> <span class="n">n_y</span><span class="p">)</span>
    <span class="c1">### END CODE HERE ###</span>
    
    <span class="c1"># Get W1, b1, W2 and b2 from the dictionary parameters.</span>
    <span class="n">W1</span> <span class="o">=</span> <span class="n">parameters</span><span class="p">[</span><span class="s2">"W1"</span><span class="p">]</span>
    <span class="n">b1</span> <span class="o">=</span> <span class="n">parameters</span><span class="p">[</span><span class="s2">"b1"</span><span class="p">]</span>
    <span class="n">W2</span> <span class="o">=</span> <span class="n">parameters</span><span class="p">[</span><span class="s2">"W2"</span><span class="p">]</span>
    <span class="n">b2</span> <span class="o">=</span> <span class="n">parameters</span><span class="p">[</span><span class="s2">"b2"</span><span class="p">]</span>
    
    <span class="c1"># Loop (gradient descent)</span>

    <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span> <span class="n">num_iterations</span><span class="p">):</span>

        <span class="c1"># Forward propagation: LINEAR -&gt; RELU -&gt; LINEAR -&gt; SIGMOID. Inputs: "X, W1, b1, W2, b2". Output: "A1, cache1, A2, cache2".</span>
        <span class="c1">### START CODE HERE ### (≈ 2 lines of code)</span>
        <span class="n">A1</span><span class="p">,</span> <span class="n">cache1</span> <span class="o">=</span> <span class="n">linear_activation_forward</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="n">W1</span><span class="p">,</span> <span class="n">b1</span><span class="p">,</span> <span class="s2">"relu"</span><span class="p">)</span>
        <span class="n">A2</span><span class="p">,</span> <span class="n">cache2</span> <span class="o">=</span> <span class="n">linear_activation_forward</span><span class="p">(</span><span class="n">A1</span><span class="p">,</span> <span class="n">W2</span><span class="p">,</span> <span class="n">b2</span><span class="p">,</span> <span class="s2">"sigmoid"</span><span class="p">)</span>
        <span class="c1">### END CODE HERE ###</span>
        
        <span class="c1"># Compute cost</span>
        <span class="c1">### START CODE HERE ### (≈ 1 line of code)</span>
        <span class="n">cost</span> <span class="o">=</span> <span class="n">compute_cost</span><span class="p">(</span><span class="n">A2</span><span class="p">,</span> <span class="n">Y</span><span class="p">)</span>
        <span class="c1">### END CODE HERE ###</span>
        
        <span class="c1"># Initializing backward propagation</span>
        <span class="n">dA2</span> <span class="o">=</span> <span class="o">-</span> <span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">divide</span><span class="p">(</span><span class="n">Y</span><span class="p">,</span> <span class="n">A2</span><span class="p">)</span> <span class="o">-</span> <span class="n">np</span><span class="o">.</span><span class="n">divide</span><span class="p">(</span><span class="mi">1</span> <span class="o">-</span> <span class="n">Y</span><span class="p">,</span> <span class="mi">1</span> <span class="o">-</span> <span class="n">A2</span><span class="p">))</span>
        
        <span class="c1"># Backward propagation. Inputs: "dA2, cache2, cache1". Outputs: "dA1, dW2, db2; also dA0 (not used), dW1, db1".</span>
        <span class="c1">### START CODE HERE ### (≈ 2 lines of code)</span>
        <span class="n">dA1</span><span class="p">,</span> <span class="n">dW2</span><span class="p">,</span> <span class="n">db2</span> <span class="o">=</span> <span class="n">linear_activation_backward</span><span class="p">(</span><span class="n">dA2</span><span class="p">,</span> <span class="n">cache2</span><span class="p">,</span> <span class="n">activation</span> <span class="o">=</span> <span class="s2">"sigmoid"</span><span class="p">)</span>
        <span class="n">dA0</span><span class="p">,</span> <span class="n">dW1</span><span class="p">,</span> <span class="n">db1</span> <span class="o">=</span> <span class="n">linear_activation_backward</span><span class="p">(</span><span class="n">dA1</span><span class="p">,</span> <span class="n">cache1</span><span class="p">,</span> <span class="n">activation</span> <span class="o">=</span> <span class="s2">"relu"</span><span class="p">)</span>
        <span class="c1">### END CODE HERE ###</span>
        
        <span class="c1"># Set grads['dWl'] to dW1, grads['db1'] to db1, grads['dW2'] to dW2, grads['db2'] to db2</span>
        <span class="n">grads</span><span class="p">[</span><span class="s1">'dW1'</span><span class="p">]</span> <span class="o">=</span> <span class="n">dW1</span>
        <span class="n">grads</span><span class="p">[</span><span class="s1">'db1'</span><span class="p">]</span> <span class="o">=</span> <span class="n">db1</span>
        <span class="n">grads</span><span class="p">[</span><span class="s1">'dW2'</span><span class="p">]</span> <span class="o">=</span> <span class="n">dW2</span>
        <span class="n">grads</span><span class="p">[</span><span class="s1">'db2'</span><span class="p">]</span> <span class="o">=</span> <span class="n">db2</span>
        
        <span class="c1"># Update parameters.</span>
        <span class="c1">### START CODE HERE ### (approx. 1 line of code)</span>
        <span class="n">parameters</span> <span class="o">=</span> <span class="n">update_parameters</span><span class="p">(</span><span class="n">parameters</span><span class="p">,</span> <span class="n">grads</span><span class="p">,</span> <span class="n">learning_rate</span><span class="p">)</span>
        <span class="c1">### END CODE HERE ###</span>

        <span class="c1"># Retrieve W1, b1, W2, b2 from parameters</span>
        <span class="n">W1</span> <span class="o">=</span> <span class="n">parameters</span><span class="p">[</span><span class="s2">"W1"</span><span class="p">]</span>
        <span class="n">b1</span> <span class="o">=</span> <span class="n">parameters</span><span class="p">[</span><span class="s2">"b1"</span><span class="p">]</span>
        <span class="n">W2</span> <span class="o">=</span> <span class="n">parameters</span><span class="p">[</span><span class="s2">"W2"</span><span class="p">]</span>
        <span class="n">b2</span> <span class="o">=</span> <span class="n">parameters</span><span class="p">[</span><span class="s2">"b2"</span><span class="p">]</span>
        
        <span class="c1"># Print the cost every 100 training example</span>
        <span class="k">if</span> <span class="n">print_cost</span> <span class="ow">and</span> <span class="n">i</span> <span class="o">%</span> <span class="mi">100</span> <span class="o">==</span> <span class="mi">0</span><span class="p">:</span>
            <span class="nb">print</span><span class="p">(</span><span class="s2">"Cost after iteration </span><span class="si">{}</span><span class="s2">: </span><span class="si">{}</span><span class="s2">"</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">i</span><span class="p">,</span> <span class="n">np</span><span class="o">.</span><span class="n">squeeze</span><span class="p">(</span><span class="n">cost</span><span class="p">)))</span>
        <span class="k">if</span> <span class="n">print_cost</span> <span class="ow">and</span> <span class="n">i</span> <span class="o">%</span> <span class="mi">100</span> <span class="o">==</span> <span class="mi">0</span><span class="p">:</span>
            <span class="n">costs</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">cost</span><span class="p">)</span>
       
    <span class="c1"># plot the cost</span>

    <span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">squeeze</span><span class="p">(</span><span class="n">costs</span><span class="p">))</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">'cost'</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">'iterations (per tens)'</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s2">"Learning rate ="</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">learning_rate</span><span class="p">))</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
    
    <span class="k">return</span> <span class="n">parameters</span>
</pre></div>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>Run the cell below to train your parameters. See if your model runs. The cost should be decreasing. It may take up to 5 minutes to run 2500 iterations. Check if the "Cost after iteration 0" matches the expected output below, if not click on the square (⬛) on the upper bar of the notebook to stop the cell and try to find your error.</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [ ]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">parameters</span> <span class="o">=</span> <span class="n">two_layer_model</span><span class="p">(</span><span class="n">train_x</span><span class="p">,</span> <span class="n">train_y</span><span class="p">,</span> <span class="n">layers_dims</span> <span class="o">=</span> <span class="p">(</span><span class="n">n_x</span><span class="p">,</span> <span class="n">n_h</span><span class="p">,</span> <span class="n">n_y</span><span class="p">),</span> <span class="n">num_iterations</span> <span class="o">=</span> <span class="mi">2500</span><span class="p">,</span> <span class="n">print_cost</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>Cost after iteration 0: 0.693049735659989
Cost after iteration 100: 0.6464320953428849
Cost after iteration 200: 0.6325140647912678
Cost after iteration 300: 0.6015024920354665
Cost after iteration 400: 0.5601966311605748
Cost after iteration 500: 0.5158304772764729
Cost after iteration 600: 0.4754901313943325
Cost after iteration 700: 0.43391631512257495
Cost after iteration 800: 0.4007977536203887
Cost after iteration 900: 0.3580705011323798
Cost after iteration 1000: 0.33942815383664127
Cost after iteration 1100: 0.3052753636196265
Cost after iteration 1200: 0.2749137728213016
Cost after iteration 1300: 0.24681768210614832
Cost after iteration 1400: 0.19850735037466086
Cost after iteration 1500: 0.17448318112556682
Cost after iteration 1600: 0.1708076297809607
Cost after iteration 1700: 0.11306524562164731
Cost after iteration 1800: 0.09629426845937152
Cost after iteration 1900: 0.08342617959726861
Cost after iteration 2000: 0.0743907870431908
Cost after iteration 2100: 0.0663074813226793
Cost after iteration 2200: 0.05919329501038171
Cost after iteration 2300: 0.05336140348560557
Cost after iteration 2400: 0.04855478562877018
</pre>
</div>
</div>
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedImage jp-OutputArea-output" tabindex="0">
<img alt="No description has been provided for this image" class="" src="data:image/png;base64,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"/>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p><strong>Expected Output</strong>:</p>
<table>
<tr>
<td> **Cost after iteration 0**</td>
<td> 0.6930497356599888 </td>
</tr>
<tr>
<td> **Cost after iteration 100**</td>
<td> 0.6464320953428849 </td>
</tr>
<tr>
<td> **...**</td>
<td> ... </td>
</tr>
<tr>
<td> **Cost after iteration 2400**</td>
<td> 0.048554785628770206 </td>
</tr>
</table>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>Good thing you built a vectorized implementation! Otherwise it might have taken 10 times longer to train this.</p>
<p>Now, you can use the trained parameters to classify images from the dataset. To see your predictions on the training and test sets, run the cell below.</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [ ]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">predictions_train</span> <span class="o">=</span> <span class="n">predict</span><span class="p">(</span><span class="n">train_x</span><span class="p">,</span> <span class="n">train_y</span><span class="p">,</span> <span class="n">parameters</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>Accuracy: 0.9999999999999998
</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p><strong>Expected Output</strong>:</p>
<table>
<tr>
<td> **Accuracy**</td>
<td> 1.0 </td>
</tr>
</table>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [ ]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">predictions_test</span> <span class="o">=</span> <span class="n">predict</span><span class="p">(</span><span class="n">test_x</span><span class="p">,</span> <span class="n">test_y</span><span class="p">,</span> <span class="n">parameters</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>Accuracy: 0.72
</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p><strong>Expected Output</strong>:</p>
<table>
<tr>
<td> **Accuracy**</td>
<td> 0.72 </td>
</tr>
</table>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p><strong>Note</strong>: You may notice that running the model on fewer iterations (say 1500) gives better accuracy on the test set. This is called "early stopping" and we will talk about it in the next course. Early stopping is a way to prevent overfitting.</p>
<p>Congratulations! It seems that your 2-layer neural network has better performance (72%) than the logistic regression implementation (70%, assignment week 2). Let's see if you can do even better with an $L$-layer model.</p>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="5---L-layer-Neural-Network">5 - L-layer Neural Network<a class="anchor-link" href="#5---L-layer-Neural-Network">¶</a></h2><p><strong>Question</strong>: Use the helper functions you have implemented previously to build an $L$-layer neural network with the following structure: <em>[LINEAR -&gt; RELU]$\times$(L-1) -&gt; LINEAR -&gt; SIGMOID</em>. The functions you may need and their inputs are:</p>
<div class="highlight"><pre><span></span><span class="k">def</span> <span class="nf">initialize_parameters_deep</span><span class="p">(</span><span class="n">layers_dims</span><span class="p">):</span>
    <span class="o">...</span>
    <span class="k">return</span> <span class="n">parameters</span> 
<span class="k">def</span> <span class="nf">L_model_forward</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="n">parameters</span><span class="p">):</span>
    <span class="o">...</span>
    <span class="k">return</span> <span class="n">AL</span><span class="p">,</span> <span class="n">caches</span>
<span class="k">def</span> <span class="nf">compute_cost</span><span class="p">(</span><span class="n">AL</span><span class="p">,</span> <span class="n">Y</span><span class="p">):</span>
    <span class="o">...</span>
    <span class="k">return</span> <span class="n">cost</span>
<span class="k">def</span> <span class="nf">L_model_backward</span><span class="p">(</span><span class="n">AL</span><span class="p">,</span> <span class="n">Y</span><span class="p">,</span> <span class="n">caches</span><span class="p">):</span>
    <span class="o">...</span>
    <span class="k">return</span> <span class="n">grads</span>
<span class="k">def</span> <span class="nf">update_parameters</span><span class="p">(</span><span class="n">parameters</span><span class="p">,</span> <span class="n">grads</span><span class="p">,</span> <span class="n">learning_rate</span><span class="p">):</span>
    <span class="o">...</span>
    <span class="k">return</span> <span class="n">parameters</span>
</pre></div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [ ]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">### CONSTANTS ###</span>
<span class="n">layers_dims</span> <span class="o">=</span> <span class="p">[</span><span class="mi">12288</span><span class="p">,</span> <span class="mi">20</span><span class="p">,</span> <span class="mi">7</span><span class="p">,</span> <span class="mi">5</span><span class="p">,</span> <span class="mi">1</span><span class="p">]</span> <span class="c1">#  4-layer model</span>
</pre></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [ ]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1"># GRADED FUNCTION: L_layer_model</span>

<span class="k">def</span> <span class="nf">L_layer_model</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="n">Y</span><span class="p">,</span> <span class="n">layers_dims</span><span class="p">,</span> <span class="n">learning_rate</span> <span class="o">=</span> <span class="mf">0.0075</span><span class="p">,</span> <span class="n">num_iterations</span> <span class="o">=</span> <span class="mi">3000</span><span class="p">,</span> <span class="n">print_cost</span><span class="o">=</span><span class="kc">False</span><span class="p">):</span><span class="c1">#lr was 0.009</span>
<span class="w">    </span><span class="sd">"""</span>
<span class="sd">    Implements a L-layer neural network: [LINEAR-&gt;RELU]*(L-1)-&gt;LINEAR-&gt;SIGMOID.</span>
<span class="sd">    </span>
<span class="sd">    Arguments:</span>
<span class="sd">    X -- data, numpy array of shape (number of examples, num_px * num_px * 3)</span>
<span class="sd">    Y -- true "label" vector (containing 0 if cat, 1 if non-cat), of shape (1, number of examples)</span>
<span class="sd">    layers_dims -- list containing the input size and each layer size, of length (number of layers + 1).</span>
<span class="sd">    learning_rate -- learning rate of the gradient descent update rule</span>
<span class="sd">    num_iterations -- number of iterations of the optimization loop</span>
<span class="sd">    print_cost -- if True, it prints the cost every 100 steps</span>
<span class="sd">    </span>
<span class="sd">    Returns:</span>
<span class="sd">    parameters -- parameters learnt by the model. They can then be used to predict.</span>
<span class="sd">    """</span>

    <span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">seed</span><span class="p">(</span><span class="mi">1</span><span class="p">)</span>
    <span class="n">costs</span> <span class="o">=</span> <span class="p">[]</span>                         <span class="c1"># keep track of cost</span>
    
    <span class="c1"># Parameters initialization. (≈ 1 line of code)</span>
    <span class="c1">### START CODE HERE ###</span>
    <span class="n">parameters</span> <span class="o">=</span> <span class="n">initialize_parameters_deep</span><span class="p">(</span><span class="n">layers_dims</span><span class="p">)</span>
    <span class="c1">### END CODE HERE ###</span>
    
    <span class="c1"># Loop (gradient descent)</span>
    <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span> <span class="n">num_iterations</span><span class="p">):</span>

        <span class="c1"># Forward propagation: [LINEAR -&gt; RELU]*(L-1) -&gt; LINEAR -&gt; SIGMOID.</span>
        <span class="c1">### START CODE HERE ### (≈ 1 line of code)</span>
        <span class="n">AL</span><span class="p">,</span> <span class="n">caches</span> <span class="o">=</span> <span class="n">L_model_forward</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="n">parameters</span><span class="p">)</span>
        <span class="c1">### END CODE HERE ###</span>
        
        <span class="c1"># Compute cost.</span>
        <span class="c1">### START CODE HERE ### (≈ 1 line of code)</span>
        <span class="n">cost</span> <span class="o">=</span> <span class="n">compute_cost</span><span class="p">(</span><span class="n">AL</span><span class="p">,</span> <span class="n">Y</span><span class="p">)</span>
        <span class="c1">### END CODE HERE ###</span>
    
        <span class="c1"># Backward propagation.</span>
        <span class="c1">### START CODE HERE ### (≈ 1 line of code)</span>
        <span class="n">grads</span> <span class="o">=</span> <span class="n">L_model_backward</span><span class="p">(</span><span class="n">AL</span><span class="p">,</span> <span class="n">Y</span><span class="p">,</span> <span class="n">caches</span><span class="p">)</span>
        <span class="c1">### END CODE HERE ###</span>
 
        <span class="c1"># Update parameters.</span>
        <span class="c1">### START CODE HERE ### (≈ 1 line of code)</span>
        <span class="n">parameters</span> <span class="o">=</span> <span class="n">update_parameters</span><span class="p">(</span><span class="n">parameters</span><span class="p">,</span> <span class="n">grads</span><span class="p">,</span> <span class="n">learning_rate</span><span class="p">)</span>
        <span class="c1">### END CODE HERE ###</span>
                
        <span class="c1"># Print the cost every 100 training example</span>
        <span class="k">if</span> <span class="n">print_cost</span> <span class="ow">and</span> <span class="n">i</span> <span class="o">%</span> <span class="mi">100</span> <span class="o">==</span> <span class="mi">0</span><span class="p">:</span>
            <span class="nb">print</span> <span class="p">(</span><span class="s2">"Cost after iteration </span><span class="si">%i</span><span class="s2">: </span><span class="si">%f</span><span class="s2">"</span> <span class="o">%</span><span class="p">(</span><span class="n">i</span><span class="p">,</span> <span class="n">cost</span><span class="p">))</span>
        <span class="k">if</span> <span class="n">print_cost</span> <span class="ow">and</span> <span class="n">i</span> <span class="o">%</span> <span class="mi">100</span> <span class="o">==</span> <span class="mi">0</span><span class="p">:</span>
            <span class="n">costs</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">cost</span><span class="p">)</span>
            
    <span class="c1"># plot the cost</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">squeeze</span><span class="p">(</span><span class="n">costs</span><span class="p">))</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">'cost'</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">'iterations (per tens)'</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s2">"Learning rate ="</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">learning_rate</span><span class="p">))</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
    
    <span class="k">return</span> <span class="n">parameters</span>
</pre></div>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>You will now train the model as a 4-layer neural network.</p>
<p>Run the cell below to train your model. The cost should decrease on every iteration. It may take up to 5 minutes to run 2500 iterations. Check if the "Cost after iteration 0" matches the expected output below, if not click on the square (⬛) on the upper bar of the notebook to stop the cell and try to find your error.</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [ ]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">parameters</span> <span class="o">=</span> <span class="n">L_layer_model</span><span class="p">(</span><span class="n">train_x</span><span class="p">,</span> <span class="n">train_y</span><span class="p">,</span> <span class="n">layers_dims</span><span class="p">,</span> <span class="n">num_iterations</span> <span class="o">=</span> <span class="mi">2500</span><span class="p">,</span> <span class="n">print_cost</span> <span class="o">=</span> <span class="kc">True</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>Cost after iteration 0: 0.771749
Cost after iteration 100: 0.672053
Cost after iteration 200: 0.648263
Cost after iteration 300: 0.611507
Cost after iteration 400: 0.567047
Cost after iteration 500: 0.540138
Cost after iteration 600: 0.527930
Cost after iteration 700: 0.465477
Cost after iteration 800: 0.369126
Cost after iteration 900: 0.391747
Cost after iteration 1000: 0.315187
Cost after iteration 1100: 0.272700
Cost after iteration 1200: 0.237419
Cost after iteration 1300: 0.199601
Cost after iteration 1400: 0.189263
Cost after iteration 1500: 0.161189
Cost after iteration 1600: 0.148214
Cost after iteration 1700: 0.137775
Cost after iteration 1800: 0.129740
Cost after iteration 1900: 0.121225
Cost after iteration 2000: 0.113821
Cost after iteration 2100: 0.107839
Cost after iteration 2200: 0.102855
Cost after iteration 2300: 0.100897
Cost after iteration 2400: 0.092878
</pre>
</div>
</div>
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedImage jp-OutputArea-output" tabindex="0">
<img alt="No description has been provided for this image" class="" src="data:image/png;base64,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"/>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p><strong>Expected Output</strong>:</p>
<table>
<tr>
<td> **Cost after iteration 0**</td>
<td> 0.771749 </td>
</tr>
<tr>
<td> **Cost after iteration 100**</td>
<td> 0.672053 </td>
</tr>
<tr>
<td> **...**</td>
<td> ... </td>
</tr>
<tr>
<td> **Cost after iteration 2400**</td>
<td> 0.092878 </td>
</tr>
</table>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [ ]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">pred_train</span> <span class="o">=</span> <span class="n">predict</span><span class="p">(</span><span class="n">train_x</span><span class="p">,</span> <span class="n">train_y</span><span class="p">,</span> <span class="n">parameters</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>Accuracy: 0.9856459330143539
</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<table>
<tr>
<td>
    **Train Accuracy**
    </td>
<td>
    0.985645933014
    </td>
</tr>
</table>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [ ]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">pred_test</span> <span class="o">=</span> <span class="n">predict</span><span class="p">(</span><span class="n">test_x</span><span class="p">,</span> <span class="n">test_y</span><span class="p">,</span> <span class="n">parameters</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>Accuracy: 0.8
</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p><strong>Expected Output</strong>:</p>
<table>
<tr>
<td> **Test Accuracy**</td>
<td> 0.8 </td>
</tr>
</table>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>Congrats! It seems that your 4-layer neural network has better performance (80%) than your 2-layer neural network (72%) on the same test set.</p>
<p>This is good performance for this task. Nice job!</p>
<p>Though in the next course on "Improving deep neural networks" you will learn how to obtain even higher accuracy by systematically searching for better hyperparameters (learning_rate, layers_dims, num_iterations, and others you'll also learn in the next course).</p>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="6)-Results-Analysis">6) Results Analysis<a class="anchor-link" href="#6)-Results-Analysis">¶</a></h2><p>First, let's take a look at some images the L-layer model labeled incorrectly. This will show a few mislabeled images.</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [ ]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">print_mislabeled_images</span><span class="p">(</span><span class="n">classes</span><span class="p">,</span> <span class="n">test_x</span><span class="p">,</span> <span class="n">test_y</span><span class="p">,</span> <span class="n">pred_test</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedImage jp-OutputArea-output" tabindex="0">
<img alt="No description has been provided for this image" class="" src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAADC8AAAFFCAYAAAB2JSbjAAAAOXRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjguMywgaHR0cHM6Ly9tYXRwbG90bGliLm9yZy/H5lhTAAAACXBIWXMAAA9hAAAPYQGoP6dpAAEAAElEQVR4nOz9ebStV1XnD8+n2+3p7z23S26bvoNgQrBCQkQCFgkq+ANRfCWJUlCWig38VPAdIChS5fBFKEQKqzRgKVIGClFEMGgCJGLoAumbm9v3555293s/zfvHNTf5ftfD3ueGHJK7z/czBmMw9/M8a83VzTXnXOvkelmWZSaEEEIIIYQQQgghhBBCCCGEEEIIIYQQQgghhBBCCLFC+M+0AkIIIYQQQgghhBBCCCGEEEIIIYQQQgghhBBCCCGEGG70xwtCCCGEEEIIIYQQQgghhBBCCCGEEEIIIYQQQgghhFhR9McLQgghhBBCCCGEEEIIIYQQQgghhBBCCCGEEEIIIYRYUfTHC0IIIYQQQgghhBBCCCGEEEIIIYQQQgghhBBCCCGEWFH0xwtCCCGEEEIIIYQQQgghhBBCCCGEEEIIIYQQQgghhFhR9McLQgghhBBCCCGEEEIIIYQQQgghhBBCCCGEEEIIIYRYUfTHC0IIIYQQQgghhBBCCCGEEEIIIYQQQgghhBBCCCGEWFH0xwtCCCGEEEIIIYQQQgghhBBCCCGEEEIIIYQQQgghhFhR9McLQgghhBBCCCGEEEIIIYQQQgghhBBCCCGEEEIIIYRYUfTHC0PAtm3b7MYbbzwp33777eZ5nt1+++1PWx2e59nv/M7vPG3lCSFWD7JRQghxashuCiGercg+CSFWC7J3QgixfGQzhRCrBdk7IcRqQLZOCLEakK0TQqwGZOvEsx398cL3yEc/+lHzPO/k/0qlkp177rn2S7/0S3b06NFnWr1T4nOf+9yqNCartd1idSAbJVYCjYUYZmQ3T39Wa7vF8CP7JFYCjYV4NiJ7J1YCjYUYVmQzT39Wa7uFOFVk705/Vmu7hTgVZOtOf1Zru4U4FWTrTn9Wa7uFOBVk605/Vmu7v5+Ez7QCw8K73/1u2759u7Xbbbvjjjvswx/+sH3uc5+z++67zyqVyvdVlxe96EXWarWsUCic0nef+9zn7EMf+lDuomu1WhaGwzld+rVbiGFBNko8nchuitWA7Obpi2yUGHZkn8TTiWymeDYjeyeeTmTvxLAjm3n6IvskxKkhe3f6InsnxPKRrTt9ka0TYvnI1p2+yNYJsXxk605fZOtWnuGcOc8AL3/5y+3yyy83M7M3vOENtmbNGnvf+95nn/nMZ+ynf/qnc79pNBpWrVafdl1837dSqfS0lvl0lyeE+P4iGyWEEKeG7KYQ4tmK7JMQYrUgeyeEEMtHNlMIsVqQvRNCrAZk64QQqwHZOiHEakC2Tojvjv9MKzCs/PAP/7CZme3evdvMzG688UYbGRmxxx57zK677jobHR21n/mZnzEzszRN7f3vf79ddNFFViqVbP369famN73J5ufnocwsy+z3fu/37Mwzz7RKpWIvfvGL7f7773fqvv32283zPLv99tvh97vuusuuu+46m5yctGq1as95znPsAx/4wEn9PvShD5mZwT9Z8zie5zl/RXT33Xfby1/+chsbG7ORkRF7yUteYv/2b/8G7zz+T+Dceeed9uu//us2PT1t1WrVXvWqV9nMzAy8u7i4aA899JAtLi4up4vtH//xH+2aa66x0dFRGxsbs+c///n28Y9//OTzr3zlK/aa17zGtmzZYsVi0TZv3my/9mu/Zq1W6+Q7g9otxLAiG3WClbJR27Zts1e84hV2xx132BVXXGGlUsl27Nhhf/EXf+G8u2vXLnvNa15jU1NTVqlU7Ad/8AftH/7hH3L77G/+5m/sPe95j5155plWKpXsJS95ie3cuXOgPo8juynEU0d28wTy7YR49iH7dAL5dbKZYviRvTuB7J3snRDLQTbzBIphhRh+ZO9OIHsnxHAjW3cC2TohhhvZuhPI1gkx3MjWnUC2TpjpX15YMR577DEzM1uzZs3J3+I4th/5kR+xq666yv7wD//w5D/98qY3vck++tGP2k033WRvfvObbffu3fbHf/zHdvfdd9udd95pURSZmdk73vEO+73f+z277rrr7LrrrrNvfetb9rKXvcy63e5AfW699VZ7xSteYRs3brRf+ZVfsQ0bNtiDDz5on/3sZ+1XfuVX7E1vepMdOnTIbr31Vvvf//t/Dyzv/vvvt6uvvtrGxsbsN37jNyyKIvvIRz5iP/RDP2Rf+tKX7AUveAG8/8u//Ms2OTlp73znO23Pnj32/ve/337pl37J/s//+T8n3/n0pz9tN910k9188812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XLbLLrvMPvnJTzrv3XrrrXbVVVfZxMSEjYyM2HnnnWdvf/vb4Z0PfvCDdtFFF1mlUrHJyUm7/PLL7eMf/zi889BDD9m+ffsGtu13fud3zPM827lzp9144402MTFh4+PjdtNNN1mz2YR34zi23/3d37WzzjrLisWibdu2zd7+9rdbp9OB97Zt22aveMUr7I477rArrrjCSqWS7dixw/7iL/5ioD6Pc/DgQfv5n/9527RpkxWLRdu+fbv9wi/8gnW7XTMzm5ubs7e+9a12ySWX2MjIiI2NjdnLX/5y+853vnOyjNtvv92e//znm5nZTTfdZJ7nmed59tGPfnTZegghnhrDbDfNZKOEOJ0ZZvskv04IsRIMs900k40SQpxAtk62TohnM8NsoxTHCiGejOzdCWTvhBhuZOtOIFsnxHAjW3cC2TohhhvZuhPI1gkz/csLK8bf/d3fmZnZz/7szz7lMj7wgQ/Yj/3Yj9nP/MzPWLfbtU984hP2mte8xj772c/a9ddfb2Zm999/v73iFa+w5zznOfbud7/bisWi7dy50+68886T5fzP//k/7c1vfrO9+tWvtl/5lV+xdrtt99xzj9111132ute97uR7F1xwgV1zzTV2++23L0u/n/zJn7Tt27fbe9/7XvvWt75l/+t//S9bt24d/PXXG97wBvvYxz5mr371q+0tb3mL3XXXXfbe977XHnzwQfv0pz8N5e3cudNe/epX28///M/bDTfcYH/+539uN954o1122WV20UUX9dXl0KFDdsUVV9jCwoK98Y1vtPPPP98OHjxon/zkJ63ZbFqhULBdu3bZ3/7t39prXvMa2759ux09etQ+8pGP2DXXXGMPPPCAbdq0yS644AJ797vfbe94xzvsjW98o1199dVmZnbllVcuq0+EEE+dYbabslFCnN4Ms316HPl1Qoink2G2m7JRQojHka2TrRPi2cww26jHURwrhDCTvXsc2TshhhvZuhPI1gkx3MjWnUC2TojhRrbuBLJ1wszMMrEiPO95z8vGx8eX/f4NN9yQbd26FX5rNpsgd7vd7OKLL85++Id/+ORvf/RHf5SZWTYzM/Ndy/7xH//x7KKLLhqog5ll11xzzcD33vnOd2Zmlv3cz/0c/P6qV70qW7NmzUn529/+dmZm2Rve8AZ4761vfWtmZtm//Mu/nPxt69atmZllX/7y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"/>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p><strong>A few types of images the model tends to do poorly on include:</strong></p>
<ul>
<li>Cat body in an unusual position</li>
<li>Cat appears against a background of a similar color</li>
<li>Unusual cat color and species</li>
<li>Camera Angle</li>
<li>Brightness of the picture</li>
<li>Scale variation (cat is very large or small in image)</li>
</ul>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="7)-Test-with-your-own-image-(optional/ungraded-exercise)">7) Test with your own image (optional/ungraded exercise)<a class="anchor-link" href="#7)-Test-with-your-own-image-(optional/ungraded-exercise)">¶</a></h2><p>Congratulations on finishing this assignment. You can use your own image and see the output of your model. To do that:
1. Click on "File" in the upper bar of this notebook, then click "Open" to go on your Coursera Hub.
2. Add your image to this Jupyter Notebook's directory, in the "images" folder
3. Change your image's name in the following code
4. Run the code and check if the algorithm is right (1 = cat, 0 = non-cat)!</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [ ]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">## START CODE HERE ##</span>
<span class="kn">import</span> <span class="nn">imageio.v3</span> <span class="k">as</span> <span class="nn">iio</span>
<span class="kn">from</span> <span class="nn">skimage.transform</span> <span class="kn">import</span> <span class="n">resize</span>
<span class="n">my_image</span> <span class="o">=</span> <span class="s2">"my_image.jpg"</span> <span class="c1"># change this to the name of your image file </span>
<span class="n">my_label_y</span> <span class="o">=</span> <span class="p">[</span><span class="mi">1</span><span class="p">]</span> <span class="c1"># the true class of your image (1 -&gt; cat, 0 -&gt; non-cat)</span>
<span class="c1">## END CODE HERE ##</span>

<span class="n">fname</span> <span class="o">=</span> <span class="s2">"images/"</span> <span class="o">+</span> <span class="n">my_image</span>
<span class="c1"># image = np.array(ndimage.imread(fname, flatten=False))</span>
<span class="n">image</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">array</span><span class="p">(</span><span class="n">iio</span><span class="o">.</span><span class="n">imread</span><span class="p">(</span><span class="n">fname</span><span class="p">))</span>
<span class="c1"># my_image = scipy.misc.imresize(image, size=(num_px,num_px)).reshape((num_px*num_px*3,1))</span>
<span class="n">my_image</span> <span class="o">=</span> <span class="n">resize</span><span class="p">(</span><span class="n">image</span><span class="p">,</span> <span class="p">(</span><span class="n">num_px</span><span class="p">,</span> <span class="n">num_px</span><span class="p">))</span><span class="o">.</span><span class="n">reshape</span><span class="p">((</span><span class="n">num_px</span><span class="o">*</span><span class="n">num_px</span><span class="o">*</span><span class="mi">3</span><span class="p">,</span><span class="mi">1</span><span class="p">))</span>
<span class="n">my_image</span> <span class="o">=</span> <span class="n">my_image</span><span class="o">/</span><span class="mf">255.</span>

<span class="n">my_predicted_image</span> <span class="o">=</span> <span class="n">predict</span><span class="p">(</span><span class="n">my_image</span><span class="p">,</span> <span class="n">my_label_y</span><span class="p">,</span> <span class="n">parameters</span><span class="p">)</span>

<span class="n">plt</span><span class="o">.</span><span class="n">imshow</span><span class="p">(</span><span class="n">image</span><span class="p">)</span>
<span class="nb">print</span> <span class="p">(</span><span class="s2">"y = "</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">squeeze</span><span class="p">(</span><span class="n">my_predicted_image</span><span class="p">))</span> <span class="o">+</span> <span class="s2">", your L-layer model predicts a </span><span class="se">\"</span><span class="s2">"</span> <span class="o">+</span> <span class="n">classes</span><span class="p">[</span><span class="nb">int</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">squeeze</span><span class="p">(</span><span class="n">my_predicted_image</span><span class="p">)),]</span><span class="o">.</span><span class="n">decode</span><span class="p">(</span><span class="s2">"utf-8"</span><span class="p">)</span> <span class="o">+</span>  <span class="s2">"</span><span class="se">\"</span><span class="s2"> picture."</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>[[0.08474424]]
Accuracy: 0.0
y = 0.0, your L-layer model predicts a "non-cat" picture.
</pre>
</div>
</div>
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedImage jp-OutputArea-output" tabindex="0">
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p><strong>References</strong>:</p>
<ul>
<li>for auto-reloading external module: <a href="http://stackoverflow.com/questions/1907993/autoreload-of-modules-in-ipython">http://stackoverflow.com/questions/1907993/autoreload-of-modules-in-ipython</a></li>
</ul>
</div>
</div>
</div>
</div>
</main>
</body>