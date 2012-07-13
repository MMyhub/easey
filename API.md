# Easing

Easing is moving from one point or zoom to another in a fluid motion, instead of just 'popping' from
place to place. It's useful for map-based storytelling, since users get a better idea of geographical
distance.

## var ease = mapbox.ease()

This creates a new object from which to do easing transitions.

### ease.from(MM.Coordinate)

Set the 'from' coordinate in this easing. The map starts from here. You don't usually need to call this, because calling `.map(mapObject)` automatically assigns `from` to the current position of the map:

    from = map.coordinate.copy();

### ease.to(MM.Coordinate)

Set the destination of the ease: this takes `MM.Coordinate`s - you can get coordinates out of other types by using `locationCoordinate` and `pointCoordinate`.

Since easey deals exclusively in Coordinates, [the reference for converting between points, locations, and coordinates in Modest Maps is essential reading](https://github.com/stamen/modestmaps-js/wiki/Point,-Location,-and-Coordinate).

### ease.zoom(value)

Set the zoom level of the `to` coordinate, so the zoom level that easey is easing to. The argument to this
function must be a number corresponding to a zoom level.

This is a convenience function for

    easey.to(easey.to().zoomTo(zoomLevel));

### ease.t(value)

Derive a point in the ease. The argument is a float between 0 and 1, in which 0 is `from` and 1 is `to`.

### ease.future(value)

Get the future of an easing transition, given a number of parts for it to be divided over.
This returns an array of `MM.Coordinate` objects representing each in-between location.
The argument to this function is a positive integer number.

This is a convenience function for calling `easey.t()` a bunch of times.

### ease.easing(value)

Set the easing curve. This takes a string as its argument. The current options are:

* 'easeIn'
* 'easeOut'
* 'easeInOut'
* 'linear'

### ease.path(value)

Set the type of path - the type of interpolation between points.

This takes a string with the current options:

* `screen`: a 'straight line' path from place to place - in the Mercator projection, this is a rhumb line
* `about`: the default path for a double-click zoom: this keeps a single coordinate in the same screen pixel over the zoom transition

### ease.run([time [, callback])

Start an _animated ease_. Both parameters are optional: if provided, `time` is
an integer number corresponding to the number of milliseconds duration,
and second argument is a `callback` - a Javascript function that
is called when the map has moved to its destination.

Tile will default to `1000` and is measured in milliseconds.

### var isRunning = ease.running()

Returns `true` or `false` depending on whether easey is currently animating the map.

### ease.stop()

Abort the currently running animation.
