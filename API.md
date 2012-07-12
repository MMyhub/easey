## `var ease = mapbox.ease()`

This creates a new object from which to do easing transitions.

### `ease.from(MM.Coordinate)`

Set the 'from' coordinate in this easing. The map starts from here. You don't usually need to call this, because calling `.map(mapObject)` automatically assigns `from` to the current position of the map:

```javascript
from = map.coordinate.copy();
```

### `ease.to(MM.Coordinate)`

Set the destination of the ease: this takes `MM.Coordinate`s - you can get coordinates out of other types by using `locationCoordinate` and `pointCoordinate`.

Since easey deals exclusively in Coordinates, [the reference for converting between points, locations, and coordinates in Modest Maps is essential reading](https://github.com/stamen/modestmaps-js/wiki/Point,-Location,-and-Coordinate).

### `ease.zoom(zoomLevel)`

Set the zoom level of the `to` coordinate, so the zoom level that easey is easing to. This is a convenience function for

```javascript
easey.to(easey.to().zoomTo(zoomLevel));
```

### `ease.t(0.5)`

Derive a point in the ease. The argument is a float between 0 and 1, in which 0 is `from` and 1 is `to`.

### `ease.future(parts)`

Get the future of an easing transition, given a number of parts for it to be divided over. This returns an array of `MM.Coordinate` objects representing each in-between location.

This is a convenience function for calling `easey.t()` a bunch of times.

### `ease.easing('easeIn', 'easeOut', 'easeInOut', 'linear')`

Set the easing. This takes a string, like `"easeIn"`

### `ease.path('about')`

This defines the type of path that easey follows:

* `screen`: a 'straight line' path from place to place - in the Mercator projection, this is a rhumb line
* `about`: the default path for a double-click zoom: this keeps a single coordinate in the same screen pixel over the zoom transition

### `ease.run([time], [callback])`

Start an _animated ease_. Both parameters are optional - `time` will default to `1000` and is measured in milliseconds.

The second argument is a `callback` - a Javascript function that is called when the map has moved to its destination.

### `var isRunning = ease.running()`

Returns `true` or `false` depending on whether easey is currently animating the map.

### `ease.stop()`

Abort the currently running animation.
