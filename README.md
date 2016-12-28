## Ace Collaborative Extensions
Enhances the [Ace Editor](https://github.com/ajaxorg/ace) by adding the ability to render cues about
what remote users are doing in the system.

## Installation

Install package with NPM and add it to your development dependencies:

```npm install --save-dev ace-collab-ext```

## Usage

### Multi Cursor Manager
The multi cursor manager allows you to easily render the cursors of other users
working in the same document.  The cursor position can be represented as either
a single linear index or as a 2-dimensional position in the form of
```{row: 0, column: 10}```.

```javascript
var editor = ace.edit("editor");
var curMgr = new AceCollabExt.AceMultiSelectionManager(editor);

// Add a new remote cursor with an id of "uid1", and a color of orange.
curMgr.addCursor("uid1", "User 1", "orange", position);

// Set cursor for "uid1" to index 10.
curMgr.setCursor("uid1", 10);

// Clear the remote cursor for "uid1" without removing it.
curMgr.clearCursor("uid1");

// Remove the remote cursor for "uid1".
curMgr.removeCursor("uid1");
```

### Multi Selection Manager
The multi selection manager allows you to easily render the selection of other
users working in the same document. Selection is represented by an array of 
AceRanges.  A single range is common for normal selection, but multiple ranges 
are needed to support block selection.

```javascript
var editor = ace.edit("editor");
var selMgr = new AceCollabExt.AceMultiSelectionManager(editor);

// Add a new remote view indicator with an id of "uid1", and a color of orange.
selMgr.addSelection("uid1", "User 1", "orange", ranges);

// Set the selection to a new range.
selMgr.setSelection("uid1", range);

// Nullify the selection without removing the marker.
selMgr.clearSelection("uid1");

// Remove the remote view indicator for "uid1".
selMgr.removeSelection("uid1");
```

### Radar View
A radar view indicates where in a document another user is looking and allows
you to easily go to the location in the document.

```javascript
var editor = ace.edit("editor");
var radarView = new AceCollabExt.RadarView("radarView", editor);

// Add a new remote view indicator with an id of "uid1", and a color of orange.
radarView.addView("uid1", "user1", "orange", 0, 20, 0);

// Set the viewport range of the indicator to span rows 10 through 40.
radarView.setViewRows("uid1", 10, 40);

// Set the row location of the cursor to line 10.
radarView.setCursoRow("uid1", 10);

// Remove the remote view indicator for "uid1".
radarView.removeView("uid1");
```