<!doctype html>
<html>
<head>
<meta charset='UTF-8'><meta name='viewport' content='width=device-width initial-scale=1'>
<title>Linux 意外操作后如何进行数据抢救.md</title><link href='http://fonts.googleapis.com/css?family=Open+Sans:400italic,700italic,700,400&subset=latin,latin-ext' rel='stylesheet' type='text/css'><style type='text/css'>html, body {overflow-x: initial !important;}.mermaid .label { color: rgb(51, 51, 51); }
.node rect, .node circle, .node ellipse, .node polygon { fill: rgb(236, 236, 255); stroke: rgb(204, 204, 255); stroke-width: 1px; }
.edgePath .path { stroke: rgb(51, 51, 51); }
.edgeLabel { background-color: rgb(232, 232, 232); }
.cluster rect { fill: rgb(255, 255, 222) !important; rx: 4 !important; stroke: rgb(170, 170, 51) !important; stroke-width: 1px !important; }
.cluster text { fill: rgb(51, 51, 51); }
.actor { stroke: rgb(204, 204, 255); fill: rgb(236, 236, 255); }
text.actor { fill: black; stroke: none; }
.actor-line { stroke: grey; }
.messageLine0 { stroke-width: 1.5; stroke: rgb(51, 51, 51); }
.messageLine1 { stroke-width: 1.5; stroke: rgb(51, 51, 51); }
#arrowhead { fill: rgb(51, 51, 51); }
#crosshead path { fill: rgb(51, 51, 51) !important; stroke: rgb(51, 51, 51) !important; }
.messageText { fill: rgb(51, 51, 51); stroke: none; }
.labelBox { stroke: rgb(204, 204, 255); fill: rgb(236, 236, 255); }
.labelText { fill: black; stroke: none; }
.loopText { fill: black; stroke: none; }
.loopLine { stroke-width: 2; stroke: rgb(204, 204, 255); }
.note { stroke: rgb(170, 170, 51); fill: rgb(255, 245, 173); }
.noteText { fill: black; stroke: none; font-family: "trebuchet ms", verdana, arial; font-size: 14px; }
.section { stroke: none; opacity: 0.2; }
.section0 { fill: rgba(102, 102, 255, 0.490196); }
.section2 { fill: rgb(255, 244, 0); }
.section1, .section3 { fill: white; opacity: 0.2; }
.sectionTitle0 { fill: rgb(51, 51, 51); }
.sectionTitle1 { fill: rgb(51, 51, 51); }
.sectionTitle2 { fill: rgb(51, 51, 51); }
.sectionTitle3 { fill: rgb(51, 51, 51); }
.sectionTitle { text-anchor: start; font-size: 11px; }
.grid .tick { stroke: lightgrey; opacity: 0.3; shape-rendering: crispEdges; }
.grid path { stroke-width: 0; }
.today { fill: none; stroke: red; stroke-width: 2px; }
.task { stroke-width: 2; }
.taskText { text-anchor: middle; font-size: 11px; }
.taskTextOutsideRight { fill: black; text-anchor: start; font-size: 11px; }
.taskTextOutsideLeft { fill: black; text-anchor: end; font-size: 11px; }
.taskText0, .taskText1, .taskText2, .taskText3 { fill: white; }
.task0, .task1, .task2, .task3 { fill: rgb(138, 144, 221); stroke: rgb(83, 79, 188); }
.taskTextOutside0, .taskTextOutside2 { fill: black; }
.taskTextOutside1, .taskTextOutside3 { fill: black; }
.active0, .active1, .active2, .active3 { fill: rgb(191, 199, 255); stroke: rgb(83, 79, 188); }
.activeText0, .activeText1, .activeText2, .activeText3 { fill: black !important; }
.done0, .done1, .done2, .done3 { stroke: grey; fill: lightgrey; stroke-width: 2; }
.doneText0, .doneText1, .doneText2, .doneText3 { fill: black !important; }
.crit0, .crit1, .crit2, .crit3 { stroke: rgb(255, 136, 136); fill: red; stroke-width: 2; }
.activeCrit0, .activeCrit1, .activeCrit2, .activeCrit3 { stroke: rgb(255, 136, 136); fill: rgb(191, 199, 255); stroke-width: 2; }
.doneCrit0, .doneCrit1, .doneCrit2, .doneCrit3 { stroke: rgb(255, 136, 136); fill: lightgrey; stroke-width: 2; cursor: pointer; shape-rendering: crispEdges; }
.doneCritText0, .doneCritText1, .doneCritText2, .doneCritText3 { fill: black !important; }
.activeCritText0, .activeCritText1, .activeCritText2, .activeCritText3 { fill: black !important; }
.titleText { text-anchor: middle; font-size: 18px; fill: black; }
.node text { font-family: "trebuchet ms", verdana, arial; font-size: 14px; }
div.mermaidTooltip { position: absolute; text-align: center; max-width: 200px; padding: 2px; font-family: "trebuchet ms", verdana, arial; font-size: 12px; background: rgb(255, 255, 222); border: 1px solid rgb(170, 170, 51); border-radius: 2px; pointer-events: none; z-index: 100; }


.CodeMirror { height: auto; }
.CodeMirror-scroll { overflow-y: hidden; overflow-x: auto; }
.CodeMirror-lines { padding: 4px 0px; }
.CodeMirror pre { }
.CodeMirror-scrollbar-filler, .CodeMirror-gutter-filler { background-color: white; }
.CodeMirror-gutters { border-right: 1px solid rgb(221, 221, 221); background-color: rgb(247, 247, 247); white-space: nowrap; }
.CodeMirror-linenumbers { }
.CodeMirror-linenumber { padding: 0px 3px 0px 5px; text-align: right; color: rgb(153, 153, 153); }
.CodeMirror div.CodeMirror-cursor { border-left: 1px solid black; z-index: 3; }
.CodeMirror div.CodeMirror-secondarycursor { border-left: 1px solid silver; }
.CodeMirror.cm-keymap-fat-cursor div.CodeMirror-cursor { width: auto; border: 0px; background: rgb(119, 238, 119); z-index: 1; }
.CodeMirror div.CodeMirror-cursor.CodeMirror-overwrite { }
.cm-tab { display: inline-block; }
.cm-s-typora-default .cm-header, .cm-s-typora-default .cm-property { color: rgb(217, 79, 138); }
.cm-s-typora-default pre.cm-header1:not(.cm-atom) :not(.cm-overlay) { font-size: 2rem; line-height: 2rem; }
.cm-s-typora-default pre.cm-header2:not(.cm-atom) :not(.cm-overlay) { font-size: 1.4rem; line-height: 1.4rem; }
.cm-s-typora-default .cm-atom, .cm-s-typora-default .cm-number { color: rgb(149, 132, 134); }
.cm-s-typora-default .cm-table-row, .cm-s-typora-default .cm-block-start { font-family: monospace; }
.cm-s-typora-default .cm-comment, .cm-s-typora-default .cm-code { color: rgb(74, 90, 159); font-family: monospace; }
.cm-s-typora-default .cm-tag { color: rgb(169, 68, 66); }
.cm-s-typora-default .cm-string { color: rgb(126, 134, 169); }
.cm-s-typora-default .cm-link { color: rgb(196, 122, 15); text-decoration: underline; }
.cm-s-typora-default .cm-variable-2, .cm-s-typora-default .cm-variable-1 { color: inherit; }
.cm-s-typora-default .cm-overlay { font-size: 1rem; font-family: monospace; }
.CodeMirror.cm-s-typora-default div.CodeMirror-cursor { border-left: 3px solid rgb(228, 98, 154); }
.cm-s-typora-default .CodeMirror-activeline-background { left: -60px; right: -30px; background: rgba(204, 204, 204, 0.2); }
.cm-s-typora-default .CodeMirror-gutters { border-right: none; background-color: inherit; }
.cm-s-typora-default .cm-trailing-space-new-line::after, .cm-startspace::after, .cm-starttab .cm-tab::after { content: "•"; position: absolute; left: 0px; opacity: 0; font-family: LetterGothicStd, monospace; }
.os-windows .cm-startspace::after, .os-windows .cm-starttab .cm-tab::after { left: -0.1em; }
.cm-starttab .cm-tab::after { content: " "; }
.cm-startspace, .cm-tab, .cm-starttab, .cm-trailing-space-a, .cm-trailing-space-b, .cm-trailing-space-new-line { font-family: monospace; position: relative; }
.cm-s-typora-default .cm-trailing-space-new-line::after { content: "↓"; opacity: 0.3; }
.cm-s-inner .cm-keyword { color: rgb(119, 0, 136); }
.cm-s-inner .cm-atom, .cm-s-inner.cm-atom { color: rgb(34, 17, 153); }
.cm-s-inner .cm-number { color: rgb(17, 102, 68); }
.cm-s-inner .cm-def { color: rgb(0, 0, 255); }
.cm-s-inner .cm-variable { color: black; }
.cm-s-inner .cm-variable-2 { color: rgb(0, 85, 170); }
.cm-s-inner .cm-variable-3 { color: rgb(0, 136, 85); }
.cm-s-inner .cm-property { color: black; }
.cm-s-inner .cm-operator { color: rgb(152, 26, 26); }
.cm-s-inner .cm-comment, .cm-s-inner.cm-comment { color: rgb(170, 85, 0); }
.cm-s-inner .cm-string { color: rgb(170, 17, 17); }
.cm-s-inner .cm-string-2 { color: rgb(255, 85, 0); }
.cm-s-inner .cm-meta { color: rgb(85, 85, 85); }
.cm-s-inner .cm-qualifier { color: rgb(85, 85, 85); }
.cm-s-inner .cm-builtin { color: rgb(51, 0, 170); }
.cm-s-inner .cm-bracket { color: rgb(153, 153, 119); }
.cm-s-inner .cm-tag { color: rgb(17, 119, 0); }
.cm-s-inner .cm-attribute { color: rgb(0, 0, 204); }
.cm-s-inner .cm-header, .cm-s-inner.cm-header { color: blue; }
.cm-s-inner .cm-quote, .cm-s-inner.cm-quote { color: rgb(0, 153, 0); }
.cm-s-inner .cm-hr, .cm-s-inner.cm-hr { color: rgb(153, 153, 153); }
.cm-s-inner .cm-link, .cm-s-inner.cm-link { color: rgb(0, 0, 204); }
.cm-negative { color: rgb(221, 68, 68); }
.cm-positive { color: rgb(34, 153, 34); }
.cm-header, .cm-strong { font-weight: bold; }
.cm-del { text-decoration: line-through; }
.cm-em { font-style: italic; }
.cm-link { text-decoration: underline; }
.cm-error { color: rgb(255, 0, 0); }
.cm-invalidchar { color: rgb(255, 0, 0); }
.cm-constant { color: rgb(38, 139, 210); }
.cm-defined { color: rgb(181, 137, 0); }
div.CodeMirror span.CodeMirror-matchingbracket { color: rgb(0, 255, 0); }
div.CodeMirror span.CodeMirror-nonmatchingbracket { color: rgb(255, 34, 34); }
.cm-s-inner .CodeMirror-activeline-background { background: inherit; }
.CodeMirror { position: relative; overflow: hidden; }
.CodeMirror-scroll { margin-bottom: -30px; margin-right: -30px; padding-bottom: 30px; padding-right: 30px; height: 100%; outline: none; position: relative; box-sizing: content-box; }
.CodeMirror-sizer { position: relative; }
.CodeMirror-vscrollbar, .CodeMirror-hscrollbar, .CodeMirror-scrollbar-filler, .CodeMirror-gutter-filler { position: absolute; z-index: 6; display: none; }
.CodeMirror-vscrollbar { right: 0px; top: 0px; overflow-x: hidden; overflow-y: scroll; }
.CodeMirror-hscrollbar { bottom: 0px; left: 0px; overflow-y: hidden; overflow-x: scroll; }
.CodeMirror-scrollbar-filler { right: 0px; bottom: 0px; }
.CodeMirror-gutter-filler { left: 0px; bottom: 0px; }
.CodeMirror-gutters { position: absolute; left: 0px; top: 0px; padding-bottom: 30px; z-index: 3; }
.CodeMirror-gutter { white-space: normal; height: 100%; box-sizing: content-box; padding-bottom: 30px; margin-bottom: -32px; display: inline-block; }
.CodeMirror-gutter-elt { position: absolute; cursor: default; z-index: 4; }
.CodeMirror-lines { cursor: text; }
.CodeMirror pre { border-radius: 0px; border-width: 0px; background: transparent; font-family: inherit; font-size: inherit; margin: 0px; white-space: pre; word-wrap: normal; color: inherit; z-index: 2; position: relative; overflow: visible; }
.CodeMirror-wrap pre { word-wrap: break-word; white-space: pre-wrap; word-break: normal; }
.CodeMirror-code pre { border-right: 30px solid transparent; width: fit-content; }
.CodeMirror-wrap .CodeMirror-code pre { border-right: none; width: auto; }
.CodeMirror-linebackground { position: absolute; left: 0px; right: 0px; top: 0px; bottom: 0px; z-index: 0; }
.CodeMirror-linewidget { position: relative; z-index: 2; overflow: auto; }
.CodeMirror-widget { }
.CodeMirror-wrap .CodeMirror-scroll { overflow-x: hidden; }
.CodeMirror-measure { position: absolute; width: 100%; height: 0px; overflow: hidden; visibility: hidden; }
.CodeMirror-measure pre { position: static; }
.CodeMirror div.CodeMirror-cursor { position: absolute; visibility: hidden; border-right: none; width: 0px; }
.CodeMirror div.CodeMirror-cursor { visibility: hidden; }
.CodeMirror-focused div.CodeMirror-cursor { visibility: inherit; }
.CodeMirror-selected { background: rgb(217, 217, 217); }
.CodeMirror-focused .CodeMirror-selected { background: rgb(215, 212, 240); }
.cm-searching { background: rgba(255, 255, 0, 0.4); }
.CodeMirror span { }
@media print { 
  .CodeMirror div.CodeMirror-cursor { visibility: hidden; }
}
.CodeMirror-lint-markers { width: 16px; }
.CodeMirror-lint-tooltip { background-color: infobackground; border: 1px solid black; border-radius: 4px; color: infotext; font-family: monospace; overflow: hidden; padding: 2px 5px; position: fixed; white-space: pre-wrap; z-index: 10000; max-width: 600px; opacity: 0; transition: opacity 0.4s; font-size: 0.8em; }
.CodeMirror-lint-mark-error, .CodeMirror-lint-mark-warning { background-position: left bottom; background-repeat: repeat-x; }
.CodeMirror-lint-mark-error { background-image: url("data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAQAAAADCAYAAAC09K7GAAAAAXNSR0IArs4c6QAAAAZiS0dEAP8A/wD/oL2nkwAAAAlwSFlzAAALEwAACxMBAJqcGAAAAAd0SU1FB9sJDw4cOCW1/KIAAAAZdEVYdENvbW1lbnQAQ3JlYXRlZCB3aXRoIEdJTVBXgQ4XAAAAHElEQVQI12NggIL/DAz/GdA5/xkY/qPKMDAwAADLZwf5rvm+LQAAAABJRU5ErkJggg=="); }
.CodeMirror-lint-marker-error, .CodeMirror-lint-marker-warning { background-position: center center; background-repeat: no-repeat; cursor: pointer; display: inline-block; height: 16px; width: 16px; vertical-align: middle; position: relative; }
.CodeMirror-lint-message-error, .CodeMirror-lint-message-warning { padding-left: 18px; background-position: left top; background-repeat: no-repeat; }
.CodeMirror-lint-marker-error, .CodeMirror-lint-message-error { background-image: url("data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAMAAAAoLQ9TAAAAHlBMVEW7AAC7AACxAAC7AAC7AAAAAAC4AAC5AAD///+7AAAUdclpAAAABnRSTlMXnORSiwCK0ZKSAAAATUlEQVR42mWPOQ7AQAgDuQLx/z8csYRmPRIFIwRGnosRrpamvkKi0FTIiMASR3hhKW+hAN6/tIWhu9PDWiTGNEkTtIOucA5Oyr9ckPgAWm0GPBog6v4AAAAASUVORK5CYII="); }
.CodeMirror-lint-marker-warning, .CodeMirror-lint-message-warning { background-image: url("data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAMAAAAoLQ9TAAAANlBMVEX/uwDvrwD/uwD/uwD/uwD/uwD/uwD/uwD/uwD6twD/uwAAAADurwD2tQD7uAD+ugAAAAD/uwDhmeTRAAAADHRSTlMJ8mN1EYcbmiixgACm7WbuAAAAVklEQVR42n3PUQqAIBBFUU1LLc3u/jdbOJoW1P08DA9Gba8+YWJ6gNJoNYIBzAA2chBth5kLmG9YUoG0NHAUwFXwO9LuBQL1giCQb8gC9Oro2vp5rncCIY8L8uEx5ZkAAAAASUVORK5CYII="); }
.CodeMirror-lint-marker-multiple { background-image: url("data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAcAAAAHCAMAAADzjKfhAAAACVBMVEUAAAAAAAC/v7914kyHAAAAAXRSTlMAQObYZgAAACNJREFUeNo1ioEJAAAIwmz/H90iFFSGJgFMe3gaLZ0od+9/AQZ0ADosbYraAAAAAElFTkSuQmCC"); background-repeat: no-repeat; background-position: right bottom; width: 100%; height: 100%; }


html { font-size: 14px; background-color: rgb(255, 255, 255); color: rgb(51, 51, 51); }
body { margin: 0px; padding: 0px; height: auto; bottom: 0px; top: 0px; left: 0px; right: 0px; font-family: "Helvetica Neue", Helvetica, Arial, sans-serif; font-size: 1rem; line-height: 1.42857; overflow-x: hidden; background: inherit; }
a:active, a:hover { outline: 0px; }
.in-text-selection, ::selection { background: rgb(181, 214, 252); text-shadow: none; }
#write { margin: 0px auto; height: auto; width: inherit; word-break: normal; word-wrap: break-word; position: relative; padding-bottom: 70px; white-space: pre-wrap; overflow-x: auto; }
.for-image #write { padding-left: 8px; padding-right: 8px; }
body.typora-export { padding-left: 30px; padding-right: 30px; }
@media screen and (max-width: 500px) { 
  body.typora-export { padding-left: 0px; padding-right: 0px; }
  .CodeMirror-sizer { margin-left: 0px !important; }
  .CodeMirror-gutters { display: none !important; }
}
.typora-export #write { margin: 0px auto; }
#write > p:first-child, #write > ul:first-child, #write > ol:first-child, #write > pre:first-child, #write > blockquote:first-child, #write > div:first-child, #write > table:first-child { margin-top: 30px; }
#write li > table:first-child { margin-top: -20px; }
img { max-width: 100%; vertical-align: middle; }
input, button, select, textarea { color: inherit; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; font-size: inherit; line-height: inherit; font-family: inherit; }
input[type="checkbox"], input[type="radio"] { line-height: normal; padding: 0px; }
::before, ::after, * { box-sizing: border-box; }
#write p, #write h1, #write h2, #write h3, #write h4, #write h5, #write h6, #write div, #write pre { width: inherit; }
#write p, #write h1, #write h2, #write h3, #write h4, #write h5, #write h6 { position: relative; }
h1 { font-size: 2rem; }
h2 { font-size: 1.8rem; }
h3 { font-size: 1.6rem; }
h4 { font-size: 1.4rem; }
h5 { font-size: 1.2rem; }
h6 { font-size: 1rem; }
p { -webkit-margin-before: 1rem; -webkit-margin-after: 1rem; -webkit-margin-start: 0px; -webkit-margin-end: 0px; }
.mathjax-block { margin-top: 0px; margin-bottom: 0px; -webkit-margin-before: 0rem; -webkit-margin-after: 0rem; }
.hidden { display: none; }
.md-blockmeta { color: rgb(204, 204, 204); font-weight: bold; font-style: italic; }
a { cursor: pointer; }
#write input[type="checkbox"] { cursor: pointer; width: inherit; height: inherit; margin: 4px 0px 0px; }
tr { break-inside: avoid; break-after: auto; }
thead { display: table-header-group; }
table { border-collapse: collapse; border-spacing: 0px; width: 100%; overflow: auto; break-inside: auto; text-align: left; }
table.md-table td { min-width: 80px; }
.CodeMirror-gutters { border-right: 0px; background-color: inherit; }
.CodeMirror { text-align: left; }
.CodeMirror-placeholder { opacity: 0.3; }
.CodeMirror pre { padding: 0px 4px; }
.CodeMirror-lines { padding: 0px; }
div.hr:focus { cursor: none; }
pre { white-space: pre-wrap; }
.CodeMirror-gutters { margin-right: 4px; }
.md-fences { font-size: 0.9rem; display: block; break-inside: avoid; text-align: left; overflow: visible; white-space: pre; background: inherit; position: relative !important; }
.md-diagram-panel { width: 100%; margin-top: 10px; text-align: center; padding-top: 0px; padding-bottom: 8px; overflow-x: auto; }
.md-fences .CodeMirror.CodeMirror-wrap { top: -1.6em; margin-bottom: -1.6em; }
.md-fences.mock-cm { white-space: pre-wrap; }
.show-fences-line-number .md-fences { padding-left: 0px; }
.show-fences-line-number .md-fences.mock-cm { padding-left: 40px; }
.footnotes { opacity: 0.8; font-size: 0.9rem; padding-top: 1em; padding-bottom: 1em; }
.footnotes + .footnotes { margin-top: -1em; }
.md-reset { margin: 0px; padding: 0px; border: 0px; outline: 0px; vertical-align: top; background: transparent; text-decoration: none; text-shadow: none; float: none; position: static; width: auto; height: auto; white-space: nowrap; cursor: inherit; -webkit-tap-highlight-color: transparent; line-height: normal; font-weight: normal; text-align: left; box-sizing: content-box; direction: ltr; }
li div { padding-top: 0px; }
blockquote { margin: 1rem 0px; }
li p, li .mathjax-block { margin: 0.5rem 0px; }
li { margin: 0px; position: relative; }
blockquote > :last-child { margin-bottom: 0px; }
blockquote > :first-child { margin-top: 0px; }
.footnotes-area { color: rgb(136, 136, 136); margin-top: 0.714rem; padding-bottom: 0.143rem; }
@media print { 
  html, body { height: 100%; }
  .typora-export * { -webkit-print-color-adjust: exact; }
  h1, h2, h3, h4, h5, h6 { break-after: avoid-page; orphans: 2; }
  p { orphans: 4; }
  html.blink-to-pdf { font-size: 13px; }
  .typora-export #write { padding-left: 1cm; padding-right: 1cm; }
  .typora-export #write::after { height: 0px; }
  @page { margin: 20mm 0mm; }
}
.footnote-line { margin-top: 0.714em; font-size: 0.7em; }
a img, img a { cursor: pointer; }
pre.md-meta-block { font-size: 0.8rem; min-height: 2.86rem; white-space: pre-wrap; background: rgb(204, 204, 204); display: block; overflow-x: hidden; }
p .md-image:only-child { display: inline-block; width: 100%; text-align: center; }
#write .MathJax_Display { margin: 0.8em 0px 0px; }
.mathjax-block { white-space: pre; overflow: hidden; width: 100%; }
p + .mathjax-block { margin-top: -1.143rem; }
.mathjax-block:not(:empty)::after { display: none; }
[contenteditable="true"]:active, [contenteditable="true"]:focus { outline: none; box-shadow: none; }
.task-list { list-style-type: none; }
.task-list-item { position: relative; padding-left: 1em; }
.task-list-item input { position: absolute; top: 0px; left: 0px; }
.math { font-size: 1rem; }
.md-toc { min-height: 3.58rem; position: relative; font-size: 0.9rem; border-radius: 10px; }
.md-toc-content { position: relative; margin-left: 0px; }
.md-toc::after, .md-toc-content::after { display: none; }
.md-toc-item { display: block; color: rgb(65, 131, 196); text-decoration: none; }
.md-toc-inner:hover { }
.md-toc-inner { display: inline-block; cursor: pointer; }
.md-toc-h1 .md-toc-inner { margin-left: 0px; font-weight: bold; }
.md-toc-h2 .md-toc-inner { margin-left: 2em; }
.md-toc-h3 .md-toc-inner { margin-left: 4em; }
.md-toc-h4 .md-toc-inner { margin-left: 6em; }
.md-toc-h5 .md-toc-inner { margin-left: 8em; }
.md-toc-h6 .md-toc-inner { margin-left: 10em; }
@media screen and (max-width: 48em) { 
  .md-toc-h3 .md-toc-inner { margin-left: 3.5em; }
  .md-toc-h4 .md-toc-inner { margin-left: 5em; }
  .md-toc-h5 .md-toc-inner { margin-left: 6.5em; }
  .md-toc-h6 .md-toc-inner { margin-left: 8em; }
}
a.md-toc-inner { font-size: inherit; font-style: inherit; font-weight: inherit; line-height: inherit; }
.footnote-line a:not(.reversefootnote) { color: inherit; }
.md-attr { display: none; }
.md-fn-count::after { content: "."; }
.md-tag { opacity: 0.5; }
.md-comment { color: rgb(162, 127, 3); opacity: 0.8; font-family: monospace; }
code { text-align: left; }
h1 .md-tag, h2 .md-tag, h3 .md-tag, h4 .md-tag, h5 .md-tag, h6 .md-tag { font-weight: initial; opacity: 0.35; }
a.md-print-anchor { border-width: initial !important; border-style: none !important; border-color: initial !important; display: inline-block !important; position: absolute !important; width: 1px !important; right: 0px !important; outline: none !important; background: transparent !important; text-decoration: initial !important; text-shadow: initial !important; }
.md-inline-math .MathJax_SVG .noError { display: none !important; }
.mathjax-block .MathJax_SVG_Display { text-align: center; margin: 1em 0em; position: relative; text-indent: 0px; max-width: none; max-height: none; min-height: 0px; min-width: 100%; width: auto; display: block !important; }
.MathJax_SVG_Display, .md-inline-math .MathJax_SVG_Display { width: auto; margin: inherit; display: inline-block !important; }
.MathJax_SVG .MJX-monospace { font-family: monospace; }
.MathJax_SVG .MJX-sans-serif { font-family: sans-serif; }
.MathJax_SVG { display: inline; font-style: normal; font-weight: normal; line-height: normal; zoom: 90%; text-indent: 0px; text-align: left; text-transform: none; letter-spacing: normal; word-spacing: normal; word-wrap: normal; white-space: nowrap; float: none; direction: ltr; max-width: none; max-height: none; min-width: 0px; min-height: 0px; border: 0px; padding: 0px; margin: 0px; }
.MathJax_SVG * { transition: none; }


@font-face { font-family: "Open Sans"; font-style: normal; font-weight: normal; src: local("Open Sans Regular"), url("./github/400.woff") format("woff"); }
@font-face { font-family: "Open Sans"; font-style: italic; font-weight: normal; src: local("Open Sans Italic"), url("./github/400i.woff") format("woff"); }
@font-face { font-family: "Open Sans"; font-style: normal; font-weight: bold; src: local("Open Sans Bold"), url("./github/700.woff") format("woff"); }
@font-face { font-family: "Open Sans"; font-style: italic; font-weight: bold; src: local("Open Sans Bold Italic"), url("./github/700i.woff") format("woff"); }
html { font-size: 16px; }
body { font-family: "Open Sans", "Clear Sans", "Helvetica Neue", Helvetica, Arial, sans-serif; color: rgb(51, 51, 51); line-height: 1.6; }
#write { max-width: 860px; margin: 0px auto; padding: 20px 30px 100px; }
#write > ul:first-child, #write > ol:first-child { margin-top: 30px; }
body > :first-child { margin-top: 0px !important; }
body > :last-child { margin-bottom: 0px !important; }
a { color: rgb(65, 131, 196); }
h1, h2, h3, h4, h5, h6 { position: relative; margin-top: 1rem; margin-bottom: 1rem; font-weight: bold; line-height: 1.4; cursor: text; }
h1:hover a.anchor, h2:hover a.anchor, h3:hover a.anchor, h4:hover a.anchor, h5:hover a.anchor, h6:hover a.anchor { text-decoration: none; }
h1 tt, h1 code { font-size: inherit; }
h2 tt, h2 code { font-size: inherit; }
h3 tt, h3 code { font-size: inherit; }
h4 tt, h4 code { font-size: inherit; }
h5 tt, h5 code { font-size: inherit; }
h6 tt, h6 code { font-size: inherit; }
h1 { padding-bottom: 0.3em; font-size: 2.25em; line-height: 1.2; border-bottom: 1px solid rgb(238, 238, 238); }
h2 { padding-bottom: 0.3em; font-size: 1.75em; line-height: 1.225; border-bottom: 1px solid rgb(238, 238, 238); }
h3 { font-size: 1.5em; line-height: 1.43; }
h4 { font-size: 1.25em; }
h5 { font-size: 1em; }
h6 { font-size: 1em; color: rgb(119, 119, 119); }
p, blockquote, ul, ol, dl, table { margin: 0.8em 0px; }
li > ol, li > ul { margin: 0px; }
hr { height: 4px; padding: 0px; margin: 16px 0px; background-color: rgb(231, 231, 231); border-width: 0px 0px 1px; border-style: none none solid; border-top-color: initial; border-right-color: initial; border-left-color: initial; border-image: initial; overflow: hidden; box-sizing: content-box; border-bottom-color: rgb(221, 221, 221); }
body > h2:first-child { margin-top: 0px; padding-top: 0px; }
body > h1:first-child { margin-top: 0px; padding-top: 0px; }
body > h1:first-child + h2 { margin-top: 0px; padding-top: 0px; }
body > h3:first-child, body > h4:first-child, body > h5:first-child, body > h6:first-child { margin-top: 0px; padding-top: 0px; }
a:first-child h1, a:first-child h2, a:first-child h3, a:first-child h4, a:first-child h5, a:first-child h6 { margin-top: 0px; padding-top: 0px; }
h1 p, h2 p, h3 p, h4 p, h5 p, h6 p { margin-top: 0px; }
li p.first { display: inline-block; }
ul, ol { padding-left: 30px; }
ul:first-child, ol:first-child { margin-top: 0px; }
ul:last-child, ol:last-child { margin-bottom: 0px; }
blockquote { border-left: 4px solid rgb(221, 221, 221); padding: 0px 15px; color: rgb(119, 119, 119); }
blockquote blockquote { padding-right: 0px; }
table { padding: 0px; word-break: initial; }
#write { overflow-x: auto; }
table tr { border-top: 1px solid rgb(204, 204, 204); background-color: white; margin: 0px; padding: 0px; }
table tr:nth-child(2n) { background-color: rgb(248, 248, 248); }
table tr th { font-weight: bold; border: 1px solid rgb(204, 204, 204); text-align: left; margin: 0px; padding: 6px 13px; }
table tr td { border: 1px solid rgb(204, 204, 204); text-align: left; margin: 0px; padding: 6px 13px; }
table tr th:first-child, table tr td:first-child { margin-top: 0px; }
table tr th:last-child, table tr td:last-child { margin-bottom: 0px; }
.CodeMirror-gutters { border-right: 1px solid rgb(221, 221, 221); }
.md-fences, code, tt { border: 1px solid rgb(221, 221, 221); background-color: rgb(248, 248, 248); border-radius: 3px; font-family: Consolas, "Liberation Mono", Courier, monospace; padding: 2px 4px 0px; font-size: 0.9em; }
.md-fences { margin-bottom: 15px; margin-top: 15px; padding: 8px 1em 6px; }
.task-list { padding-left: 0px; }
.task-list-item { padding-left: 32px; }
.task-list-item input { top: 3px; left: 8px; }
@media screen and (min-width: 914px) { 
}
@media print { 
  html { font-size: 13px; }
  table, pre { break-inside: avoid; }
  pre { word-wrap: break-word; }
}
.md-fences { background-color: rgb(248, 248, 248); }
#write pre.md-meta-block { padding: 1rem; font-size: 85%; line-height: 1.45; background-color: rgb(247, 247, 247); border: 0px; border-radius: 3px; color: rgb(119, 119, 119); margin-top: 0px !important; }
.mathjax-block > .code-tooltip { bottom: 0.375rem; }
#write > h3.md-focus::before { left: -1.5625rem; top: 0.375rem; }
#write > h4.md-focus::before { left: -1.5625rem; top: 0.285714rem; }
#write > h5.md-focus::before { left: -1.5625rem; top: 0.285714rem; }
#write > h6.md-focus::before { left: -1.5625rem; top: 0.285714rem; }
.md-image > .md-meta { border: 1px solid rgb(221, 221, 221); background-color: rgb(248, 248, 248); border-radius: 3px; font-family: Consolas, "Liberation Mono", Courier, monospace; padding: 2px 4px 0px; font-size: 0.9em; color: inherit; }
.md-tag { color: inherit; }
.md-toc { margin-top: 20px; padding-bottom: 20px; }
#typora-quick-open { border: 1px solid rgb(221, 221, 221); background-color: rgb(248, 248, 248); }
#typora-quick-open-item { background-color: rgb(250, 250, 250); border-color: rgb(254, 254, 254) rgb(229, 229, 229) rgb(229, 229, 229) rgb(238, 238, 238); border-style: solid; border-width: 1px; }
#md-notification::before { top: 10px; }
.on-focus-mode blockquote { border-left-color: rgba(85, 85, 85, 0.117647); }
header, .context-menu, .megamenu-content, footer { font-family: "Segoe UI", Arial, sans-serif; }






</style>
</head>
<body class='typora-export' >
<div  id='write'  class = 'is-node'><h1><a name='header-c2355' class='md-header-anchor '></a>Linux 意外操作后如何进行数据抢救</h1><p><img style="vertical-align: middle;" src="http://images2015.cnblogs.com/blog/952608/201701/952608-20170125120304628-720092779.png" width="800px"></p><p>在 GUI 中使用  <code>shift + delete</code>  组合键或是 CLI 下使用 <code>rm -rf</code> 删除选项，这个文件并没有从硬盘（或是其它存储设备）上彻底销毁。当它文件被删除以后，<code>inode</code> 的数据指针部分被清零，仅仅是从系统的目录结构中被移除，但是这个文件仍然存在你磁盘中的某个 <code>block</code> 物理位置上。（ <code>ls -li</code> 或 <code>stat</code> 查询一个文件所对应的 <a href='https://en.wikipedia.org/wiki/Inode'>inode</a> 的元信息数据。 ）。</p><p>注意：<strong><a href='https://en.wikipedia.org/wiki/RAID'>独立硬盘冗余阵列</a></strong>（<strong>RAID</strong>, <strong>R</strong>edundant <strong>A</strong>rray of <strong>I</strong>ndependent <strong>D</strong>isks）损坏或数据丢失，不在本次范围。</p><hr /><p><strong>Linux 系统管理员守则中有这么一条：“慎用 rm -rf 命令，除非你知道此命令所带来的后果“</strong></p><p> <br></p><h2><a name='header-c2368' class='md-header-anchor '></a>一、实验环境</h2><h3><a name='header-c2369' class='md-header-anchor '></a>1、工具</h3><p>VMware® Workstation 12 Pro 12.5.2 build-4638234</p><p>CentOS-6.5-x86_64-bin-DVD1.iso</p><h3><a name='header-c2374' class='md-header-anchor '></a>2、约定</h3><p>1、所有操作全部在虚拟机环境下完成，使用CentOS操作系统。关闭SELinux！</p><p>2、故障模拟如下：</p><pre class='md-fences mock-cm' style='display:block;position:relative'># df -hT
* 显示当前系统配置情况，不同测试工具不同环境（每张图可体现是一个崭新的CentOS）
# openssl rand -base64 {num} -out {mount_path/filename}
  使用 openssl 数据工具生成 {num} 位随机数。
# md5sum {mount_path/filename}
* 使用 md5sum 验证工具打印 {mount_path/filename} MD5信息
# rm -rf {mount_path/filename}
  执行 rm -rf {mount_path/filename}
  
&quot;#&quot; 表示权限 &quot;root&quot;、&quot;*&quot; 表示必须截图体现，另特殊情况下也截图。心情好也截图 :)</pre><p>3、测试情况下包括后续内容皆为 “配置好环境变量” 情况下。</p><pre class='md-fences mock-cm' style='display:block;position:relative'>0、不设置，可这么执行
   {ProgramName}
   /usr/bin/{ProgramName}
   /usr/local/{ProgramName}/bin/{ProgramName} --help
1、设置别名，可永久生效
   alias {ProgramName}=&quot;usr/local/{ProgramName}/bin/{ProgramName}&quot;
2、设置环境变量，临时生效
   export PATH=$PATH:/usr/local/{ProgramName}/bin
3、设置程序软链接，永久生效
   ln -s /usr/local/{ProgramName}/bin/{ProgramName}  /usr/bin/{ProgramName}</pre><p>4、实验记录详情：</p><pre class='md-fences mock-cm' style='display:block;position:relative'>1、数据恢复：
   单个文件（约定2已进行说明）
   文件夹/目录（参见：https://github.com/erlinux/RecoverDateProject/tree/master/test）
2、更多包括：
   格式支持、界面支持、恢复时长、恢复效果。（详情见文末表格）</pre><p>5、模拟企业真实情况：</p><pre class='md-fences mock-cm' style='display:block;position:relative'>1、磁盘可卸除挂载
2、恢复程序编译安装</pre><p>6、测试框架皆为：</p><pre class='md-fences mock-cm' style='display:block;position:relative'>1、通过文件系统的 inode 值（一般是 2 ）来获取文件系统信息。
2、通过上步骤所得出的结论使用 inode 编号以及 filename 进行恢复。
3、通过程序自带的文件夹恢复 或 时间前后恢复 来恢复所删除的数据。
4、通过上述三种步骤所展现的情况（包括其他测试）进行详细的记录用于对比。</pre><h3><a name='header-c2392' class='md-header-anchor '></a>3、备注</h3><p>1、为帮助大家更好理解已进行中文译化。</p><p>2、本人仅仅是一名学生，文章不当的地方还请指出。</p><p>3、最后祝各位新年快乐。鸡年大吉大利、心想事成、身体健康。（ 就当新年礼物吧 ^_^ ）</p><p><br><br></p><h2><a name='header-c2401' class='md-header-anchor '></a>二、恢复工具</h2><p>在恢复数据前，要弄清楚俩个概念：inode（索引节点） 和 block （数据块）</p><p>block 用于储存数据，inode 用于存储数据属性信息。inode 为每个文件进行信息索引，所以就有了 inode 的数值。</p><div class="md-diagram-panel" mdtype="math_block"><svg id="mermaidChart1333" width="574" xmlns="http://www.w3.org/2000/svg" height="162" viewBox="0 0 594 182" style="height: 222px;"><g><g class="output"><g class="clusters"></g><g class="edgePaths"><g class="edgePath" style="opacity: 1;"><path class="path" d="M96,38L169,38L242,38" marker-end="url(#arrowhead15017)" style="stroke: #333; stroke-width: 1.5px;fill:none"></path><defs><marker id="arrowhead15017" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" style="fill: #333"></path></marker></defs></g><g class="edgePath" style="opacity: 1;"><path class="path" d="M304,38L377,38L464,38" marker-end="url(#arrowhead15018)" style="stroke: #333; stroke-width: 1.5px;fill:none"></path><defs><marker id="arrowhead15018" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" style="fill: #333"></path></marker></defs></g><g class="edgePath" style="opacity: 1;"><path class="path" d="M96,124L169,124L249,124" marker-end="url(#arrowhead15019)" style="stroke: #333; stroke-width: 1.5px;fill:none"></path><defs><marker id="arrowhead15019" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" style="fill: #333"></path></marker></defs></g><g class="edgePath" style="opacity: 1;"><path class="path" d="M297,124L377,124L450,124" marker-end="url(#arrowhead15020)" style="stroke: #333; stroke-width: 1.5px;fill:none"></path><defs><marker id="arrowhead15020" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" style="fill: #333"></path></marker></defs></g></g><g class="edgeLabels"><g class="edgeLabel" transform="" style="opacity: 1;"><g transform="translate(0,0)" class="label"><rect rx="0" ry="0" width="0" height="0" style="fill:#e8e8e8;"></rect><text><tspan xml:space="preserve" dy="1em" x="1"></tspan></text></g></g><g class="edgeLabel" transform="translate(377,38)" style="opacity: 1;"><g transform="translate(-48,-10.796875)" class="label"><rect rx="0" ry="0" width="95.984375" height="21.5625" style="fill:#e8e8e8;"></rect><text><tspan xml:space="preserve" dy="1em" x="1">组合数据成为</tspan></text></g></g><g class="edgeLabel" transform="translate(169,124)" style="opacity: 1;"><g transform="translate(-48,-10.796875)" class="label"><rect rx="0" ry="0" width="95.984375" height="21.5625" style="fill:#e8e8e8;"></rect><text><tspan xml:space="preserve" dy="1em" x="1">保存索引信息</tspan></text></g></g><g class="edgeLabel" transform="" style="opacity: 1;"><g transform="translate(0,0)" class="label"><rect rx="0" ry="0" width="0" height="0" style="fill:#e8e8e8;"></rect><text><tspan xml:space="preserve" dy="1em" x="1"></tspan></text></g></g></g><g class="nodes"><g class="node" id="file" transform="translate(58,38)" style="opacity: 1;"><rect rx="5" ry="5" x="-38" y="-18" width="76" height="36"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-28,-8)"><text><tspan xml:space="preserve" dy="1em" x="1">读写索引</tspan></text></g></g></g><g class="node" id="date" transform="translate(273,38)" style="opacity: 1;"><rect rx="5" ry="5" x="-31" y="-18" width="62" height="36"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-21,-8)"><text><tspan xml:space="preserve" dy="1em" x="1">数据块</tspan></text></g></g></g><g class="node" id="标准文件" transform="translate(502,38)" style="opacity: 1;"><rect rx="0" ry="0" x="-38" y="-18" width="76" height="36"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-28,-8)"><text><tspan xml:space="preserve" dy="1em" x="1">标准文件</tspan></text></g></g></g><g class="node" id="移除文件" transform="translate(58,124)" style="opacity: 1;"><rect rx="0" ry="0" x="-38" y="-18" width="76" height="36"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-28,-8)"><text><tspan xml:space="preserve" dy="1em" x="1">移除文件</tspan></text></g></g></g><g class="node" id="save" transform="translate(273,124)" style="opacity: 1;"><rect rx="5" ry="5" x="-24" y="-18" width="48" height="36"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-14,-8)"><text><tspan xml:space="preserve" dy="1em" x="1">日志</tspan></text></g></g></g><g class="node" id="删除索引指针" transform="translate(502,124)" style="opacity: 1;"><rect rx="0" ry="0" x="-52" y="-18" width="104" height="36"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-42,-8)"><text><tspan xml:space="preserve" dy="1em" x="1">删除索引指针</tspan></text></g></g></g></g></g></g></svg></div><hr /><h3><a name='header-c2408' class='md-header-anchor '></a><a href='http://extundelete.sourceforge.net' target='_blank' title='完成'>extundelete</a></h3><p><img style="vertical-align: middle;" src="http://images2015.cnblogs.com/blog/952608/201701/952608-20170125200144456-989913250.png" width="800px"></p><p><center>注意：即便不能实现重新只读挂载当前数据盘，也绝对不能在需要恢复文件的目录下进行操作。</center></p><h4><a name='header-c2413' class='md-header-anchor '></a>1 -&gt; 安装</h4><pre class='md-fences mock-cm' style='display:block;position:relative'># curl -O https://nchc.dl.sourceforge.net/project/extundelete/extundelete/0.2.4/extundelete-0.2.4.tar.bz2
# tar -jxvf extundelete-0.2.4.tar.bz2 &amp;&amp; cd extundelete-0.2.4 
# ./configure --prefix=/usr/local/extundelete
-------------------
configure: error: C++ compiler cannot create executables
# yum install gcc gcc-c++ -y
configure: error: Can&#39;t find ext2fs library
# yum install e2fsprogs.x86_64 e2fsprogs-devel.x86_64 e2fsprogs-libs.x86_64  -y
-------------------
make &amp;&amp; make install</pre><h4><a name='header-c2415' class='md-header-anchor '></a>2 --&gt; 选项</h4><pre class='md-fences mock-cm' style='display:block;position:relative'>extundelete --help
用法: extundelete [选项] [--] 设备-文件
选项:
  --version, -[vV]       打印版本并且正常退出.
  --help,                打印帮助并且正常退出.
  --[superblock](http://baike.baidu.com/view/1102790.htm)           
                         除了剩余的内容之外，还打印超级块的内容。
                         默认选项
  --journal              显示日志内容
  --after dtime          只处理在 &#39;dtime&#39; 后被删除的条目
  --before dtime         只处理在 &#39;dtime&#39; 前被删除的条目
功能:
  --inode ino            显示 &#39;ino&#39; 的 索引节点 信息
  --block blk            显示 &#39;blk&#39; 的    块   信息
  --restore-inode ino[,ino,...]
                         恢复具有已知索引节点号 &#39;ino&#39;,
                         已恢复的文件在当前目录的RECOVERED_FILES文件夹里创建
                         而文件的索引节点号作为扩展(ie:file.12345)
  --restore-file &#39;path&#39;  将恢复文件 &#39;path&#39;. &#39;path&#39; 是相对于根分区而言的，并且不以 &#39;/&#39; 开头
                         已恢复的文件在当前目录的 &#39;RECOVERED_FILES/path&#39;.
  --restore-files &#39;path&#39; 列出将在 &#39;path&#39; 恢复的文件.
                         每个文件名格式应该与选项 --restore-file 相同，并且每行都应该有一个.
  --restore-directory &#39;path&#39;
                         恢复文件夹 &#39;path&#39;.
                         &#39;path&#39; 是相对于文件系统的根目录而言的.
                         已恢复的文件夹输出目录在&#39;path&#39;。
  --restore-all          尝试去恢复一切
  -j journal             从一个已命名的文件读取外部日志
  -b blocknumber         当打开系统文件时，使用一个块数字备份超级快.
  -B blocksize           当打开系统文件，使用 blocksize 作为一个块大小.
                         这个数字应该以 bytes 为单位.
  --log 0                程序静默执行
  --log filename         记录所有消息到文件.
  --log D1=0,D2=filename 自定义控制以逗号分隔的日志消息
示例如下:                 列出选项. Dn 必须是 info,warn 或者 error 中一个。
   --log info,error      略去 ‘=name’ 信息中的结果
   --log warn=0          将指定的级别记录到计算机控制台.如果变量为 &#39;=0&#39;,指定的级别记录将被关闭.
   --log error=filename  如果变量为&#39;=filename&#39;，写入具有该级别的消息到文件名.
   -o directory          保存恢复的文件到指定目录.
                         默认情况下，恢复的文件被创建在 &#39;RECOVERED_FILES&#39; 文件夹.</pre><pre class='md-fences mock-cm' style='display:block;position:relative'>extundelete /dev/sdb1 --inode 2
查找可恢复的数据信息，标记为Deleted状态的是已经删除的文件或目录。</pre><p><img style="vertical-align: middle;" src="http://images2015.cnblogs.com/blog/952608/201701/952608-20170126105005769-348282016.png" width="800px"></p><pre class='md-fences mock-cm' style='display:block;position:relative'>extundelete /dev/sdb1 --restore-inode 12,13
extundelete /dev/sdb1 --restore-file fstab
extundelete  /dev/sdb1 --after 1293877800  --restore-all
在当前目录的 &quot;RECOVERED_FILES&quot; 下恢复恢复1293877800秒后的所有误删文件
Note: date -d &quot;Jan 01 18:30 2011&quot; +%s</pre><h4><a name='header-c2421' class='md-header-anchor '></a>3 --&gt; 成功</h4><h5><a name='header-c2422' class='md-header-anchor '></a>① 模拟故障</h5><pre class='md-fences mock-cm' style='display:block;position:relative'>2e4c997cdbdf81b9419297ec156960e0  /mnt/extundelete/extundelete.asdasfsafds-test</pre><p><img src='http://images2015.cnblogs.com/blog/952608/201701/952608-20170126235729487-785407136.png' alt='' /></p><h5><a name='header-c2426' class='md-header-anchor '></a>② 故障恢复</h5><h6><a name='header-c2427' class='md-header-anchor '></a>文件</h6><p><img src='http://images2015.cnblogs.com/blog/952608/201701/952608-20170126235909753-624622922.png' alt='' /></p><p><img src='http://images2015.cnblogs.com/blog/952608/201701/952608-20170127000156316-56092849.png' alt='' /></p><h6><a name='header-c2432' class='md-header-anchor '></a>目录</h6><p><img src='http://images2015.cnblogs.com/blog/952608/201701/952608-20170127120722409-1429922714.png' alt='' /></p><p><img src='http://images2015.cnblogs.com/blog/952608/201701/952608-20170127130434925-1351915548.png' alt='' /></p><hr /><h3><a name='header-c2438' class='md-header-anchor '></a><a href='http://code.google.com/p/ext3grep/' target='_blank' title='完成'>ext3grep</a></h3><p><img style="vertical-align: middle;" src="http://images2015.cnblogs.com/blog/952608/201701/952608-20170126122707222-1732017307.png" width="800px"></p><h4><a name='header-c2441' class='md-header-anchor '></a>1 -&gt; 安装</h4><pre class='md-fences mock-cm' style='display:block;position:relative'># wget --no-check-certificate https://github.com/erlinux/RecoverProject/raw/master/soft/ext3grep/ext3grep-0.10.2.zip
Note:please use wget to download file,curl download will be fail.it&#39;s hard to say 
# unzip ext3grep-0.10.2.zip &amp;&amp; cd ext3grep-0.10.2
# ./configure --prefix=/usr/local/ext3grep
-------------------
configure: error: no acceptable C compiler found in $PATH
# yum -y install gcc
configure: error: C++ preprocessor &quot;/lib/cpp&quot; fails sanity check
# yum -y install gcc-c++
configure: error: Missing headers. Please install the package e2fslibs-dev from e2fsprogs, or http://e2fsprogs.sourceforge.net for the upstream tar-ball.
# yum install -y epel-release &amp;&amp; yum install ext2fs  blkid  e2p  uuid
-------------------
# make &amp;&amp; make install</pre><h4><a name='header-c2443' class='md-header-anchor '></a>2 --&gt;选项</h4><pre class='md-fences mock-cm' style='display:block;position:relative'>Running ext3grep version 0.10.2
用法: /usr/local/ext3grep/bin/ext3grep [选项] [--] 设备-文件
选项:
  --version, -[vV]       打印版本并且正常退出.
  --help,                打印帮助并且正常退出.
  --superblock           除了剩余的内容之外，还打印超级块的内容。
                         默认选项
  --print                打印目录块inode号，如果有。
  --ls                   打印目录每个条目只有一行。
                         这个选项通常需要打开过滤。
  --accept filen         允许 &#39;filen&#39; 作为合法文件名，可多次使用
                         如果改变任何 --accept 你必须删除
                         BOTH stage* 文件!
  --accept-all           接受一切作为文件名
  --journal              显示日志内容
  --show-path-inodes     显示路径的每个目录inode号。
过滤:
  --group grp            只处理组 &#39;grp&#39;。
  --directory            只处理目录索引节点。
  --after dtime          仅&#39;dtime&#39; 或之后删除的条目。
  --before dtime         仅&#39;dtime&#39; 或之前删除的条目。
  --deleted              只显示/处理已删除条目。
  --allocated            只显示/处理指定的 inodes/blocks.
  --unallocated          只显示/处理重新分配的 inodes/blocks.
  --reallocated          不限制 inodes 重新分配的条目。
                         如果条目已删除，inode 已分配，文件类型与 dir 条目和 inode 的不同时。Inodes                                  经仔细考虑会被 &#39;重新分配&#39; 
  --zeroed-inodes        不限制 zeroed 索引接点。
                         无论此选项，链接(links)条目都始终显示。
  --depth depth          处理目录递归的深度 &#39;depth&#39;
动作:
  --inode-to-block ino   打印块，使得 inode 包含&#39;ino&#39;
  --inode ino            显示 inode 信息 &#39;ino&#39;.
                         如果使用 --ls 并且 inode 是一个目录，那么过滤器应用于文件夹条目。
                         如果你不使用 --ls 那么 --print 是默认的。
  --block blk            显示块信息 &#39;blk&#39;.
                         如果使用 --ls 并且块是目录的第一个块，那么过滤器应用于目录条目
                         如果你不使用 --ls 那么 --print 是默认的。
  --histogram=[atime|ctime|mtime|dtime|group]
                         根据给定的规格生成树状图。
                         使用 atime，ctime,或者 mtime 将改变 --after and --before 意思
  --journal-block jblk   显示日志块信息 &#39;jblk&#39;.
  --journal-transaction seq
                         用连续的数字&#39;seq&#39; 显示处理信息
  --dump-names           将文件路径写入标准输出
                         这意味着 --ls 但限制它的输出。
  --search-start str     查找以固定字符串&#39;str&#39;开头的块
  --search str           查找包含固定字符串 &quot;str&quot; 的块。
  --search-inode blk     查找Find inodes that refer to block &#39;blk&#39;.
  --search-zeroed-inodes 返回分配为零的 inode 条目表。
  --inode-dirblock-table dir
                         为目录路径为 &#39;dir&#39; 找到 block 号和每个已使用的 inodes 节点打印一个表
  --show-journal-inodes ino
                         始终在日志显示 inode &#39;ino&#39;副本
  --restore-inode ino[@seqnr][,ino[@seqnr],...]
                         恢复具有已知 inode 号的文件。
                         恢复文件将被创建在./RESTORED_FILES/
                         而文件的索引节点号作为扩展(ie:file.12345)
                         除非 &#39;@seqnr&#39; 提供使用了序列号的日志条目，不然的话使用最后一个条目。
                         在一个文件被重写或被删节这种情况下你可以使用这个，而不是删除。
  --restore-file &#39;path&#39; [--restore-file &#39;path&#39; ...]
                         将恢复文件 &#39;path&#39;. &#39;path&#39; 是相对于根分区而言的，并且不以 &#39;/&#39; 开头 (
                         它必须成为由 --dump-names 返回的路径之一 ).
                         已恢复的目录、文件、被创建在&#39;RESTORED_FILES/path&#39;.
  --restore-all          虽然还是 --restore-file 但是程序会尝试去恢复一切.
                         推荐使用 --after 。因为尝试恢复很旧的文件会导致他们被硬链接到最近删除的文件
                         并且如此操作输出量的可能性就越大。
  --show-hardlinks       显示所有由俩个或多个共享的 inodes</pre><pre class='md-fences mock-cm' style='display:block;position:relative'>ext3grep /dev/sdb1 --inode 2
查看 indoe 为 2 的目录
ext3grep /dev/sdb1 --dump-names
列出 /dev/sdb1 下的所有文件
ext3grep /dev/sdb1 --restore-all
恢复 /dev/sdb1 下所有文件</pre><h4><a name='header-c2446' class='md-header-anchor '></a>3 --&gt;成功</h4><h5><a name='header-c2447' class='md-header-anchor '></a>① 模拟故障</h5><pre class='md-fences mock-cm' style='display:block;position:relative'>289f73b0b41489dfaa98f5eb094a382b  /mnt/ext3grep/ext3grep_ashndiasdnaind_test</pre><p><img src='http://images2015.cnblogs.com/blog/952608/201701/952608-20170127151357003-1885366985.png' alt='' /></p><h5><a name='header-c2451' class='md-header-anchor '></a>② 故障恢复</h5><h6><a name='header-c2452' class='md-header-anchor '></a>文件</h6><p><img src='http://images2015.cnblogs.com/blog/952608/201701/952608-20170127153713612-1368050497.png' alt='' /></p><p><img src='http://images2015.cnblogs.com/blog/952608/201701/952608-20170127154413441-1243965744.png' alt='' /></p><h6><a name='header-c2457' class='md-header-anchor '></a>目录</h6><p><font color=red>ext3grep 并没有提供恢复目录选项（也许我没发现），但是可以曲线救国法使用before&amp;after进行文件夹恢复<br>另外计算秒数的 date 命令可以这么使用<code>$(date -d &quot;-1 hour&quot; +%s)</code></font></p><p><img src='http://images2015.cnblogs.com/blog/952608/201701/952608-20170128014016581-1703252120.png' alt='' /></p><p>其他</p><p><img src='http://images2015.cnblogs.com/blog/952608/201701/952608-20170126195459362-132848160.png' alt='' /></p><p><font color=yellow>该工具仅能恢复 ext3 文件系统。</font></p><hr /><h3><a name='header-c2469' class='md-header-anchor '></a><a href='http://ext4magic.sourceforge.net/ext4magic_en.html' target='_blank' title='完成'>ext4magic</a></h3><p><img src='http://images2015.cnblogs.com/blog/952608/201701/952608-20170127174432831-2067567417.png' alt='' /></p><h4><a name='header-c2472' class='md-header-anchor '></a>1 -&gt; 安装</h4><pre class='md-fences mock-cm' style='display:block;position:relative'># wget --no-check-certificate https://github.com/erlinux/RecoverProject/raw/master/soft/ext4magic/ext4magic-0.3.2.tar.gz
# tar -zxvf ext4magic-0.3.2.tar.gz &amp;&amp; cd ext4magic-0.3.2
# ./configure --prefix=/usr/local/ext4magic/
---------------
configure: error: no acceptable C compiler found in $PATH
# yum install gcc -y
configure: error: You must install the develop packages &quot;ext2fs , blkid , e2p , uuid&quot; to build ext4magic
# 无法解决，改用 home_robi-1 仓库安装
----------------
yum --enablerepo=home_robi-1 install ext4magic  -y
WebSite:http://download.opensuse.org/repositories/home:/robi-1/CentOS_CentOS-6/</pre><h4><a name='header-c2474' class='md-header-anchor '></a>2 --&gt;选项</h4><pre class='md-fences mock-cm' style='display:block;position:relative'>  范例
              打印目录的 Inode，这有一些可能性。

               # ext4magic /dev/sda3 -f /
               # ext4magic /dev/sda3 -I 2

              在第一示例中，输出的是文件系统根目录实际索引节点。
              在第二示例中，输入路径名称也是根目录。 即：Inode 2                                            


               # ext4magic /tmp/filesystem.iso -f / -T -x

              使用文件系统镜像 &quot;/tmp/filesystem.iso&quot;,
              搜索并且打印所有 Block 包括根 Inode，并且打印所有不同的 Inode。(包含数据块的块列表)
              如果是目录，那么还要为每个 Inode 打印目录的内容。
              
              
               #  ext4magic /tmp/filesystem.iso -j /tmp/journal.backup -I 8195
              -t 182                                                          

              使用文件系统镜像 &quot;/tmp/filesystem.iso&quot; 并且读取从外部日志 &quot;/tmp/journal.backup&quot; 
              从日志处理 182 编号的 Inode 8195 编号。
     
     
               #  ext4magic /dev/sda3 -f user1/Documents -a $(date -d &quot;-3 day&quot;
              +%s) -b $(date -d &quot;-2 day&quot; +%s)                                 

              打印俩到三天前被删除的路径名 &quot;user1/Documents&quot; 的索引数据。 
              如果它是一个目录，那么（也打印）这个目录的内容。
              如果在日志找不到旧目录 blocks，目录内容将从文件系统真实内容。         



       简单实例

               # ext4magic /dev/sda3 -r -f user1/picture/cim01234.jpg -d /tmp

              恢复文件刚刚被删除 &quot;/home/user1/picture/cim01234.jpg&quot; .
              文件系统已正常挂载 &quot;/home&quot;.文件路径规定从指定的文件系统根目录并不是整个 Linux 根目录
              不卸载文件系统是不可能的，文件将被写在 &quot;/tmp/user1/picture/cim01234.jpg&quot;                     

               # ext4magic /dev/sda3 -r

              尝试恢复在24小时前删除的所有文件，文件写在&quot;./RECOVERDIR/&quot;内                                   



               # ext4magic /dev/sda3 -R -a $(date -d &quot;-5day&quot; +%s)

              尝试恢复所有文件，即使如果他们有些已经被重写，也能恢复所有没有删除的文件。
              删除发生在四天前。                             



               # ext4magic /dev/sda3 -M -d /home/recover

              尝试多阶段的恢复所有文件在文件系统已经 &quot;rm -rf *&quot;.
              文件写入  &quot;/home/recover&quot;.
              (on ext4: in this version skipped the last step.)              



               #  ext4magic  /dev/sda3 -RQ -f user1/Dokuments -a 1274210280 -b
              1274211280 -d /mnt/testrecover

              尝试恢复目录结构 &quot;user1/Dokuments/&quot;. &quot;-b&quot; 时间戳，你必须设置删除前的文件，
              &quot;-a&quot; 时间戳阻止找到旧的文件版本。这只会更好的工作。
              如果你有创建或删除文件在 &quot;-b&quot; 时间戳。（它会被）写入目录 &quot;/mnt/testrecover&quot;
              如果只有少数文件恢复，同时尝试不用选项 -Q



               #  ext4magic  /home/filesystem.iso -Lx  -f user1 | grep &quot;jpg&quot; &gt;
              ./tmpfile

               #  ext4magic   /home/filesystem.iso   -i   ./tmpfile   -r   -d
              /mnt/testrecover

              尝试只恢复所有从目录结构&quot;user1/&quot;，删除的文件在文件名具有 &quot;jpg&quot; (超过 24 小时)  
              并且写入进 &quot;/mnt/testrecover&quot;  - 使用一个临时文件 &quot;./tmpfile&quot; 用于文件名列表。


BUGS
       直接使用当前可读写的日志打开文件系统会读取产生坏块。
       这个坏块提供程序错误结果和不真实的结果。
       因此你应该永不使用这种文件系统，直接处于开放读写下的日志
       如果有必要，使用挂载过的文件系统，创建文件系统日志副本并且使用 -j 选项。


作者
       Roberto Maar
译者
       jiwenkang

更多参见
       debugfs (8) , e2fsck (8)</pre><pre class='md-fences mock-cm' style='display:block;position:relative'>-I             -&gt; inode        索引节点，+数字
-f             -&gt; path         目录位置，+位置

ext4magic {sdx} -r/-R             -&gt;        recover all (程度较低)
ext4magic {sdx} -M                -&gt;        recover all (程度很强)
ext4magic {sdx} -rf {path/files}  -&gt;        recover file
ext4magic {sdx} -d  {path}        -&gt;        recover to diresotry</pre><h4><a name='header-c2477' class='md-header-anchor '></a>3 --&gt;成功</h4><h6><a name='header-c2478' class='md-header-anchor '></a>① 模拟故障</h6><pre class='md-fences mock-cm' style='display:block;position:relative'>c466f4672a18ee37ba5197e4d264d6ef  /mnt/ext4magic1/ext4magic1_111111
33dd6934d4a26c7fcb8a829c98fba1fb  /mnt/ext4magic2/ext4magic1_222222</pre><p><img src='http://images2015.cnblogs.com/blog/952608/201701/952608-20170128000938128-918466979.png' alt='' /></p><h6><a name='header-c2482' class='md-header-anchor '></a>② 故障恢复</h6><h6><a name='header-c2483' class='md-header-anchor '></a>文件</h6><p><img src='http://images2015.cnblogs.com/blog/952608/201701/952608-20170128004435191-554772506.png' alt='' /></p><h6><a name='header-c2486' class='md-header-anchor '></a>目录</h6><p><img src='http://images2015.cnblogs.com/blog/952608/201701/952608-20170128010655612-174899050.png' alt='' /></p><hr /><h3><a name='header-c2490' class='md-header-anchor '></a>[foremost][foremost]</h3><p><img src='http://images2015.cnblogs.com/blog/952608/201701/952608-20170128154953441-1465119725.png' alt='' /></p><h4><a name='header-c2493' class='md-header-anchor '></a>1 -&gt; 安装</h4><pre class='md-fences mock-cm' style='display:block;position:relative'># wget --no-check-certificate https://github.com/erlinux/RecoverProject/raw/master/soft/foremost/foremost-1.5.7.tar.gz
# tar -zxvf foremost-1.5.7.tar.gz  &amp;&amp; cd foremost-1.5.7
# make
------------------
make: gcc：command not found
# yum -y install gcc
------------------
# make install</pre><h4><a name='header-c2495' class='md-header-anchor '></a>2 --&gt; 选项</h4><pre class='md-fences mock-cm' style='display:block;position:relative'>foremost version 1.5.7 by Jesse Kornblum, Kris Kendall, and Nick Mikus.
$ foremost [-v|-V|-h|-T|-Q|-q|-a|-w-d] [-t &lt;type&gt;] [-s &lt;blocks&gt;] [-k &lt;size&gt;] 
	[-b &lt;size&gt;] [-c &lt;file&gt;] [-o &lt;dir&gt;] [-i &lt;file] 

-V  - 显示版权信息并退出。
-t  - 列出文件类型 (-t jpeg,pdf ...) 
-d  - 间接打开块检测 (for UNIX file-systems) 
-i  - 指定输入文件 (默认标准输入) 
-a  - 写入所有头，不执行错误检测 (已损坏的文件) 
-w  - 只写入审计文件，不要将任何检测到的文件写入磁盘
-o  - 设置输出目录 (默认标准输出)
-c  - 设置需要使用的配置文件 (默认 foremost.conf)
-q  - 开启安静模式.搜索在 512 字节范围执行。
-Q  - 开启安静模式.禁止内容输出。
-v  - 详细模式.屏幕显示所有日志信息。、</pre><pre class='md-fences mock-cm' style='display:block;position:relative'>Foremost 支持恢复如下格式：avi, bmp, dll, doc, exe, gif, htm, jar, jpg, mbd, mov, mpg, pdf, png, ppt, rar, rif, sdw, sx, sxc, sxi, sxw, vis, wav, wmv, xls, zip。</pre><hr /><h3><a name='header-c2507' class='md-header-anchor '></a>[TestDisk][photoRec]</h3><p><img src='http://images2015.cnblogs.com/blog/952608/201701/952608-20170128182807519-211435341.png' alt='' /></p><h4><a name='header-c2510' class='md-header-anchor '></a>1 -&gt; 安装</h4><pre class='md-fences mock-cm' style='display:block;position:relative'># wget --no-check-certificate  https://raw.githubusercontent.com/erlinux/RecoverProject/master/soft/testdisk/testdisk-7.0.linux26-x86_64.tar.bz2
# tar -jxvf testdisk-7.0.linux26-x86_64 
# ./testdisk-7.0/testdisk_static</pre><h4><a name='header-c2512' class='md-header-anchor '></a>2 --&gt; 选项</h4><pre class='md-fences mock-cm' style='display:block;position:relative'>Use arrow keys to select, then press Enter key:
&gt;[ Create ] Create a new log file
 [ Append ] Append information to log file
 [ No Log ] Don&#39;t record anything

使用箭头键选择，然后按Enter键：
&gt;[ 创建 ] 创建一个新日志文件
 [ 附加 ] 将信息附加到日志文件
 [ 为空 ] 不使用日志记录任何内容
 
注意：必须正确检测磁盘容量才能成功恢复。
如果上面列出的磁盘大小不正确，请检查HD跳线设置，审查BIOS。以及安装最新的操作系统补丁和磁盘驱动程序。</pre><pre class='md-fences mock-cm' style='display:block;position:relative'>Please select the partition table type, press Enter when done.
&gt;[Intel  ] Intel/PC partition
 [EFI GPT] EFI GPT partition map (Mac i386, some x86_64...)
 [Humax  ] Humax partition table
 [Mac    ] Apple partition map
 [None   ] Non partitioned media
 [Sun    ] Sun Solaris partition
 [XBox   ] XBox partition
 [Return ] Return to disk selection

请选择分区表类型，完成后按Enter键。
&gt;[英特尔  ] 英特尔/ PC分区
 [EFI GPT] EFI GPT 分区map (Mac i386, 某些 x86_64...)
 [Humax  ] Humax 分区表
 [Mac    ] Apple 分区map
 [None   ] Non 分区介质
 [Sun    ] Sun Solaris 分区
 [XBox   ] XBox 分区
 [返回   ] 回到磁盘选择
 
提示：已检测到Intel分区表类型。
注意：不要为只有单个分区的介质选择“None”。 很少将磁盘设置为“未分区”。</pre><pre class='md-fences mock-cm' style='display:block;position:relative'>&gt;[ Analyse  ] Analyse current partition structure and search for lost partitions
 [ Advanced ] Filesystem Utils
 [ Geometry ] Change disk geometry
 [ Options  ] Modify options
 [ Quit     ] Return to disk selection

 [ 分析 ] 分析当前分区结构并搜索丢失的分区
 [ 高级 ] 文件系统实用程序
 [3D参数] 更改磁盘3D参数（Disk Geometry)，即磁头数（Heads），柱面数（Cylinders），扇区数（Sectors）
&gt;[ 选项 ] 选项修改
 [ 退出 ] 回到磁盘选择
 
 注意：恢复成功需要正确的磁盘3D参数。如果它认为分区3D参数不匹配, &#39;Analyse&#39;进程可能会给出一些警告.
 专家模式 : No
 分区对齐 : Yes
 数据转储 : No</pre><pre class='md-fences mock-cm' style='display:block;position:relative'> 专家模式 : No 分区对齐 : Yes 数据转储 : No</pre><hr /><h3><a name='header-c2523' class='md-header-anchor '></a>三、综合展示</h3><table><thead><tr><th style='text-align:center;' >功能\名字</th><th style='text-align:center;' >extundelete</th><th style='text-align:center;' >ext3grep</th><th style='text-align:center;' >ext4magic</th></tr></thead><tbody><tr><td style='text-align:center;' >分区支持</td><td style='text-align:center;' >ext3<br>ext4</td><td style='text-align:center;' >ext3</td><td style='text-align:center;' >ext3<br>ext4</td></tr><tr><td style='text-align:center;' >扫描时长</td><td style='text-align:center;' >3s</td><td style='text-align:center;' >3s</td><td style='text-align:center;' >0s</td></tr><tr><td style='text-align:center;' >恢复时长</td><td style='text-align:center;' >2s</td><td style='text-align:center;' >1s</td><td style='text-align:center;' >1s</td></tr><tr><td style='text-align:center;' >界面支持</td><td style='text-align:center;' >CLI</td><td style='text-align:center;' >CLI</td><td style='text-align:center;' >CLI</td></tr><tr><td style='text-align:center;' >恢复程度</td><td style='text-align:center;' >100%</td><td style='text-align:center;' >100%</td><td style='text-align:center;' >100%</td></tr><tr><td style='text-align:center;' >程序优势</td><td style='text-align:center;' >支持了ext3和ext4</td><td style='text-align:center;' >输出信息比较完整具体<br>对专业人士帮助较大</td><td style='text-align:center;' >支持格式多<br>输出信息规范<br>前俩者的加强升级版</td></tr><tr><td style='text-align:center;' >总体评价</td><td style='text-align:center;' >♥♥♥</td><td style='text-align:center;' >♥♥</td><td style='text-align:center;' >♥♥♥♥♥</td></tr></tbody></table></div>
</body>
</html>