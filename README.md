# mapbox-gl-opacity 

mapbox-gl-opacity is a Mapbox GL JS plugin that makes multiple tile layers transparent.  
[Mapbox GL JS Plugins](https://docs.mapbox.com/mapbox-gl-js/plugins)  
[npm](https://www.npmjs.com/package/mapbox-gl-opacity)  

<br>

Browser Support
- Chrome
- Firefox
- Safari

<br>

## Usage  

![mapbox-gl-opacity](./img/mapbox-gl-opacity.gif)

<br>

### Demo  

[demo](https://dayjournal.github.io/mapbox-gl-opacity)

<br>

### Option  

```javascript
// addControl Option

// The position of the control (one of the map corners).
position: 'top-left' or 'top-right' or 'bottom-left' or 'bottom-right'


// OpacityControl Option

// Baselayers settings
baseLayers: {
    m_mono: "MIERUNE Mono",
    m_color: "MIERUNE Color",
}

// Overlayers settings
overLayers: {
    o_std: "OpenStreetMap",
    t_pale: "GSI Pale",
    t_ort: "GSI Ort"
}

// Transparent slide bar settings (true or false)
opacityControl: true
```

<br>

### Example

./docs

index.html
```html
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>mapbox-gl-opacity example</title>

    <script src="https://api.tiles.mapbox.com/mapbox-gl-js/v1.5.0/mapbox-gl.js"></script>
    <link href="https://api.tiles.mapbox.com/mapbox-gl-js/v1.5.0/mapbox-gl.css" rel="stylesheet">

    <script src="plugin/mapbox-gl-opacity/dist/mapbox-gl-opacity.js"></script>
    <link href="plugin/mapbox-gl-opacity/dist/mapbox-gl-opacity.css" rel="stylesheet">

    <link href="css/style.css" rel="stylesheet">

</head>
<body>

    <div id="map"></div>
    <script src="js/app.js"></script>

</body>
</html>
```

style.css
```css
html, body {
    height: 100%;
    padding: 0;
    margin: 0;
}

#map {
    z-index: 0;
    height: 100%;
}
```

app.js
```javascript
// MIERUNE MONO
let map = new mapboxgl.Map({
    container: "map",
    style: {
        version: 8,
        sources: {
            m_mono: {
                type: "raster",
                tiles: ["https://tile.mierune.co.jp/mierune_mono/{z}/{x}/{y}.png"],
                tileSize: 256,
                attribution: "Maptiles by <a href='http://mierune.co.jp/' target='_blank'>MIERUNE</a>, under CC BY. Data by <a href='http://osm.org/copyright' target='_blank'>OpenStreetMap</a> contributors, under ODbL."
            }
        },
        layers: [{
            id: "m_mono",
            type: "raster",
            source: "m_mono",
            minzoom: 0,
            maxzoom: 18
        }]
    },
    center: [139.7670, 35.6810],
    zoom: 10
});

map.on("load", function() {
    // MIERUNE Color
    map.addSource("m_color", {
        type: "raster",
        tiles: ["https://tile.mierune.co.jp/mierune/{z}/{x}/{y}.png"],
        tileSize: 256
    });
    map.addLayer({
        id: "m_color",
        type: "raster",
        source: "m_color",
        minzoom: 0,
        maxzoom: 18
    });

    // OpenStreetMap
    map.addSource("o_std", {
        type: "raster",
        tiles: [
            "https://a.tile.openstreetmap.org/{z}/{x}/{y}.png",
            "https://b.tile.openstreetmap.org/{z}/{x}/{y}.png"
        ],
        tileSize: 256
    });
    map.addLayer({
        id: "o_std",
        type: "raster",
        source: "o_std",
        minzoom: 0,
        maxzoom: 18
    });

    // GSI Pale
    map.addSource("t_pale", {
        type: "raster",
        tiles: ["https://cyberjapandata.gsi.go.jp/xyz/pale/{z}/{x}/{y}.png"],
        tileSize: 256
    });
    map.addLayer({
        id: "t_pale",
        type: "raster",
        source: "t_pale",
        minzoom: 0,
        maxzoom: 18
    });

    // GSI Ort
    map.addSource("t_ort", {
        type: "raster",
        tiles: ["https://cyberjapandata.gsi.go.jp/xyz/ort/{z}/{x}/{y}.jpg"],
        tileSize: 256
    });
    map.addLayer({
        id: "t_ort",
        type: "raster",
        source: "t_ort",
        minzoom: 0,
        maxzoom: 18
    });

    // BaseLayer
    const mapBaseLayer = {
        m_mono: "MIERUNE Mono",
        m_color: "MIERUNE Color",
    };

    // OverLayer
    const mapOverLayer = {
        o_std: "OpenStreetMap",
        t_pale: "GSI Pale",
        t_ort: "GSI Ort"
    };

    // OpacityControl
    let Opacity = new OpacityControl({
        baseLayers: mapBaseLayer,
        overLayers: mapOverLayer,
        opacityControl: true
    });
    map.addControl(Opacity, 'top-right');

    // NavigationControl
    let nc = new mapboxgl.NavigationControl();
    map.addControl(nc, 'top-left');
});
```

<br>

### Example - npm

Start Mapbox GL JS easily. [Mapbox GL JS, webpack]  
[mapboxgljs-starter](https://github.com/dayjournal/mapboxgljs-starter) 

Install package
```bash
npm install mapbox-gl-opacity
```

main.js
```javascript
// CSS import
import "mapbox-gl/dist/mapbox-gl.css";
import "mapbox-gl-opacity/dist/mapbox-gl-opacity.css";
import "./css/style.css";

// JS import
import 'mapbox-gl-opacity';
import './js/script.js';
```

script.js
```javascript
// MIERUNE MONO
let map = new mapboxgl.Map({
    container: "map",
    style: {
        version: 8,
        sources: {
            m_mono: {
                type: "raster",
                tiles: ["https://tile.mierune.co.jp/mierune_mono/{z}/{x}/{y}.png"],
                tileSize: 256,
                attribution: "Maptiles by <a href='http://mierune.co.jp/' target='_blank'>MIERUNE</a>, under CC BY. Data by <a href='http://osm.org/copyright' target='_blank'>OpenStreetMap</a> contributors, under ODbL."
            }
        },
        layers: [{
            id: "m_mono",
            type: "raster",
            source: "m_mono",
            minzoom: 0,
            maxzoom: 18
        }]
    },
    center: [139.7670, 35.6810],
    zoom: 10
});

map.on("load", function() {
    // MIERUNE Color
    map.addSource("m_color", {
        type: "raster",
        tiles: ["https://tile.mierune.co.jp/mierune/{z}/{x}/{y}.png"],
        tileSize: 256
    });
    map.addLayer({
        id: "m_color",
        type: "raster",
        source: "m_color",
        minzoom: 0,
        maxzoom: 18
    });

    // OpenStreetMap
    map.addSource("o_std", {
        type: "raster",
        tiles: [
            "https://a.tile.openstreetmap.org/{z}/{x}/{y}.png",
            "https://b.tile.openstreetmap.org/{z}/{x}/{y}.png"
        ],
        tileSize: 256
    });
    map.addLayer({
        id: "o_std",
        type: "raster",
        source: "o_std",
        minzoom: 0,
        maxzoom: 18
    });

    // GSI Pale
    map.addSource("t_pale", {
        type: "raster",
        tiles: ["https://cyberjapandata.gsi.go.jp/xyz/pale/{z}/{x}/{y}.png"],
        tileSize: 256
    });
    map.addLayer({
        id: "t_pale",
        type: "raster",
        source: "t_pale",
        minzoom: 0,
        maxzoom: 18
    });

    // GSI Ort
    map.addSource("t_ort", {
        type: "raster",
        tiles: ["https://cyberjapandata.gsi.go.jp/xyz/ort/{z}/{x}/{y}.jpg"],
        tileSize: 256
    });
    map.addLayer({
        id: "t_ort",
        type: "raster",
        source: "t_ort",
        minzoom: 0,
        maxzoom: 18
    });

    // BaseLayer
    const mapBaseLayer = {
        m_mono: "MIERUNE Mono",
        m_color: "MIERUNE Color",
    };

    // OverLayer
    const mapOverLayer = {
        o_std: "OpenStreetMap",
        t_pale: "GSI Pale",
        t_ort: "GSI Ort"
    };

    // OpacityControl
    let Opacity = new OpacityControl({
        baseLayers: mapBaseLayer,
        overLayers: mapOverLayer,
        opacityControl: true
    });
    map.addControl(Opacity, 'top-right');

    // NavigationControl
    let nc = new mapboxgl.NavigationControl();
    map.addControl(nc, 'top-left');
});
```

<br>

## License
MIT

Copyright (c) 2019 Yasunori Kirimoto

<br>

---

<br>

### Japanese

<br>

# mapbox-gl-opacity 

mapbox-gl-opacityは、複数のタイルレイヤーを透過するMapbox GL JSのプラグインです。   
[Mapbox GL JS Plugins](https://docs.mapbox.com/mapbox-gl-js/plugins)  
[npm](https://www.npmjs.com/package/mapbox-gl-opacity)  

<br>

対応ブラウザ
- Chrome
- Firefox
- Safari

<br>

## 使用方法  

![mapbox-gl-opacity](./img/mapbox-gl-opacity.gif)

<br>

### デモ  

[デモ](https://dayjournal.github.io/mapbox-gl-opacity)

<br>

### オプション  

```javascript
// addControlのオプション

//コントロールの配置設定。(デフォルト:右上配置)
position: 'top-left' or 'top-right' or 'bottom-left' or 'bottom-right'


// OpacityControlのオプション

// 背景レイヤ設定
baseLayers: {
    m_mono: "MIERUNE Mono",
    m_color: "MIERUNE Color",
}

// オーバーレイヤ設定
overLayers: {
    o_std: "OpenStreetMap",
    t_pale: "GSI Pale",
    t_ort: "GSI Ort"
}

// 透過度スライドバー表示/非表示設定 (trueまたはfalse)
opacityControl: true
```

<br>

### 例

./docs

index.html
```html
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>mapbox-gl-opacity example</title>

    <script src="https://api.tiles.mapbox.com/mapbox-gl-js/v1.5.0/mapbox-gl.js"></script>
    <link href="https://api.tiles.mapbox.com/mapbox-gl-js/v1.5.0/mapbox-gl.css" rel="stylesheet">

    <script src="plugin/mapbox-gl-opacity/dist/mapbox-gl-opacity.js"></script>
    <link href="plugin/mapbox-gl-opacity/dist/mapbox-gl-opacity.css" rel="stylesheet">

    <link href="css/style.css" rel="stylesheet">

</head>
<body>

    <div id="map"></div>
    <script src="js/app.js"></script>

</body>
</html>
```

style.css
```css
html, body {
    height: 100%;
    padding: 0;
    margin: 0;
}

#map {
    z-index: 0;
    height: 100%;
}
```

app.js
```javascript
// MIERUNE MONO
let map = new mapboxgl.Map({
    container: "map",
    style: {
        version: 8,
        sources: {
            m_mono: {
                type: "raster",
                tiles: ["https://tile.mierune.co.jp/mierune_mono/{z}/{x}/{y}.png"],
                tileSize: 256,
                attribution: "Maptiles by <a href='http://mierune.co.jp/' target='_blank'>MIERUNE</a>, under CC BY. Data by <a href='http://osm.org/copyright' target='_blank'>OpenStreetMap</a> contributors, under ODbL."
            }
        },
        layers: [{
            id: "m_mono",
            type: "raster",
            source: "m_mono",
            minzoom: 0,
            maxzoom: 18
        }]
    },
    center: [139.7670, 35.6810],
    zoom: 10
});

map.on("load", function() {
    // MIERUNE Color
    map.addSource("m_color", {
        type: "raster",
        tiles: ["https://tile.mierune.co.jp/mierune/{z}/{x}/{y}.png"],
        tileSize: 256
    });
    map.addLayer({
        id: "m_color",
        type: "raster",
        source: "m_color",
        minzoom: 0,
        maxzoom: 18
    });

    // OpenStreetMap
    map.addSource("o_std", {
        type: "raster",
        tiles: [
            "https://a.tile.openstreetmap.org/{z}/{x}/{y}.png",
            "https://b.tile.openstreetmap.org/{z}/{x}/{y}.png"
        ],
        tileSize: 256
    });
    map.addLayer({
        id: "o_std",
        type: "raster",
        source: "o_std",
        minzoom: 0,
        maxzoom: 18
    });

    // GSI Pale
    map.addSource("t_pale", {
        type: "raster",
        tiles: ["https://cyberjapandata.gsi.go.jp/xyz/pale/{z}/{x}/{y}.png"],
        tileSize: 256
    });
    map.addLayer({
        id: "t_pale",
        type: "raster",
        source: "t_pale",
        minzoom: 0,
        maxzoom: 18
    });

    // GSI Ort
    map.addSource("t_ort", {
        type: "raster",
        tiles: ["https://cyberjapandata.gsi.go.jp/xyz/ort/{z}/{x}/{y}.jpg"],
        tileSize: 256
    });
    map.addLayer({
        id: "t_ort",
        type: "raster",
        source: "t_ort",
        minzoom: 0,
        maxzoom: 18
    });

    // BaseLayer
    const mapBaseLayer = {
        m_mono: "MIERUNE Mono",
        m_color: "MIERUNE Color",
    };

    // OverLayer
    const mapOverLayer = {
        o_std: "OpenStreetMap",
        t_pale: "GSI Pale",
        t_ort: "GSI Ort"
    };

    // OpacityControl
    let Opacity = new OpacityControl({
        baseLayers: mapBaseLayer,
        overLayers: mapOverLayer,
        opacityControl: true
    });
    map.addControl(Opacity, 'top-right');

    // NavigationControl
    let nc = new mapboxgl.NavigationControl();
    map.addControl(nc, 'top-left');
});
```

<br>

### 例 - npm

Mapbox GL JSを手軽に始める [Mapbox GL JS, webpack]  
[mapboxgljs-starter](https://github.com/dayjournal/mapboxgljs-starter) 

パッケージインストール
```bash
npm install mapbox-gl-opacity
```

main.js
```javascript
// CSS import
import "mapbox-gl/dist/mapbox-gl.css";
import "mapbox-gl-opacity/dist/mapbox-gl-opacity.css";
import "./css/style.css";

// JS import
import 'mapbox-gl-opacity';
import './js/script.js';
```

script.js
```javascript
// MIERUNE MONO
let map = new mapboxgl.Map({
    container: "map",
    style: {
        version: 8,
        sources: {
            m_mono: {
                type: "raster",
                tiles: ["https://tile.mierune.co.jp/mierune_mono/{z}/{x}/{y}.png"],
                tileSize: 256,
                attribution: "Maptiles by <a href='http://mierune.co.jp/' target='_blank'>MIERUNE</a>, under CC BY. Data by <a href='http://osm.org/copyright' target='_blank'>OpenStreetMap</a> contributors, under ODbL."
            }
        },
        layers: [{
            id: "m_mono",
            type: "raster",
            source: "m_mono",
            minzoom: 0,
            maxzoom: 18
        }]
    },
    center: [139.7670, 35.6810],
    zoom: 10
});

map.on("load", function() {
    // MIERUNE Color
    map.addSource("m_color", {
        type: "raster",
        tiles: ["https://tile.mierune.co.jp/mierune/{z}/{x}/{y}.png"],
        tileSize: 256
    });
    map.addLayer({
        id: "m_color",
        type: "raster",
        source: "m_color",
        minzoom: 0,
        maxzoom: 18
    });

    // OpenStreetMap
    map.addSource("o_std", {
        type: "raster",
        tiles: [
            "https://a.tile.openstreetmap.org/{z}/{x}/{y}.png",
            "https://b.tile.openstreetmap.org/{z}/{x}/{y}.png"
        ],
        tileSize: 256
    });
    map.addLayer({
        id: "o_std",
        type: "raster",
        source: "o_std",
        minzoom: 0,
        maxzoom: 18
    });

    // GSI Pale
    map.addSource("t_pale", {
        type: "raster",
        tiles: ["https://cyberjapandata.gsi.go.jp/xyz/pale/{z}/{x}/{y}.png"],
        tileSize: 256
    });
    map.addLayer({
        id: "t_pale",
        type: "raster",
        source: "t_pale",
        minzoom: 0,
        maxzoom: 18
    });

    // GSI Ort
    map.addSource("t_ort", {
        type: "raster",
        tiles: ["https://cyberjapandata.gsi.go.jp/xyz/ort/{z}/{x}/{y}.jpg"],
        tileSize: 256
    });
    map.addLayer({
        id: "t_ort",
        type: "raster",
        source: "t_ort",
        minzoom: 0,
        maxzoom: 18
    });

    // BaseLayer
    const mapBaseLayer = {
        m_mono: "MIERUNE Mono",
        m_color: "MIERUNE Color",
    };

    // OverLayer
    const mapOverLayer = {
        o_std: "OpenStreetMap",
        t_pale: "GSI Pale",
        t_ort: "GSI Ort"
    };

    // OpacityControl
    let Opacity = new OpacityControl({
        baseLayers: mapBaseLayer,
        overLayers: mapOverLayer,
        opacityControl: true
    });
    map.addControl(Opacity, 'top-right');

    // NavigationControl
    let nc = new mapboxgl.NavigationControl();
    map.addControl(nc, 'top-left');
});
```

<br>

## ライセンス
MIT

Copyright (c) 2019 Yasunori Kirimoto

<br>