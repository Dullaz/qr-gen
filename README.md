qr-image
========


Updated version of [qr-image](https://github.com/alexeyten/qr-image) repo that seems to have been abandoned

Re-introduced Pako over zlib

Overview
--------

  * TBD

Installing
-----

```shell
npm install qr-gen
```

Usage
-----

Example:
```javascript
var qr = require('qr-gen');

var qr_svg = qr.image('I love QR!', { type: 'svg' });
qr_svg.pipe(require('fs').createWriteStream('i_love_qr.svg'));

var svg_string = qr.imageSync('I love QR!', { type: 'svg' });
```

Example For generate images in client side:
```javascript in your app.js
var qr = require('qr-gen');
router.get('/qr', function(){
  var code = qr.image('http://www.google.com', { type: 'png' });
  res.setHeader('Content-type', 'image/png');  //sent qr image to client side
  code.pipe(res);
});
```
then in the html files:
```
<img src="/qr" alt="qrcode">
```

[More examples](./examples)

`qr = require('qr-gen')`

### Methods

  * `qr.image(text, [ec_level | options])` — Readable stream with image data;
  * `qr.imageSync(text, [ec_level | options])` — string with image data. (Buffer for `png`);
  * `qr.svgObject(text, [ec_level | options])` — object with SVG path and size;
  * `qr.matrix(text, [ec_level])` — 2D array of booleans. __Y__ is indexed first (e.g. `[y][x]` NOT `[x][y]`), `[0][0]` is the top left, and `true` means black.


### Options

  * `text` — text to encode;
  * `ec_level` — error correction level. One of `L`, `M`, `Q`, `H`. Default `M`.
  * `options` — image options object:
    * `ec_level` — default `M`.
    * `type` — image type. Possible values `png` (default), `svg`, `pdf` and `eps`.
    * `size` (png and svg only) — size of one module in pixels. Default `5` for png and `undefined` for svg.
    * `margin` — white space around QR image in modules. Default `4` for `png` and `1` for others.
    * `customize` (only png) — function to customize qr bitmap before encoding to PNG.
    * `parse_url` (experimental, default `false`) — try to optimize QR-code for URLs.
