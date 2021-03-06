leonardo
========

A minimalist image filter library for javascript

## Available filters
The following filters have been implemented:
* greyscale (using [luminance](http://en.wikipedia.org/wiki/Luma_%28video%29))
* sepia (using [w3c filters sepia definition](http://www.w3.org/TR/filter-effects/#sepiaEquivalent))
* popart (still in development)
* vivid (makes the colors more vivid)
* polaroid (makes the photo a bit overexposed like if it had been taken with a polaroid)

## Usage
### In the browser

Replace an image by a filtered version:
```javascript
var image = document.getElementById('my-image');
var filteredCanvas = leonardo.applyFilter(image, 'greyscale');
image.src = filteredCanvas.toDataURL();
```
### In node
```javascript
var Canvas = require('canvas'),
    Image  = Canvas.Image,
    leonardo = require('../leonardo.js'),
    fs = require('fs');

fs.readFile("~/Pictures/marilyn.jpg", function (err, imgbuff) {
  var img = new Image();
  img.src = imgbuff;
  img.onload = function() {
      var filtered = leonardo.applyFilter(img, "vivid");
      var out = fs.createWriteStream("marilyn-vivid.jpg");
      filtered.jpegStream().pipe(out);
  };
});
```

## Dependencies
### In the browser
None
### In node
* [node-canvas](https://www.npmjs.org/package/canvas)
