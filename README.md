# nicodinh:mapbox

Mapbox.js for [Meteor](https://www.meteor.com/) apps.

Version matrix:

Mapbox JS | Mapbox GL
----------|----------
`2.2.2`   | `0.11.1`

## Install

    $ cd to/my/meteor/project
    $ mkdir packages # ensure that packages folder exists
    $ git clone https://github.com/nicodinh/meteor-mapbox.git packages/nicodinh:mapbox
    $ meteor add nicodinh:mapbox

## Supported plugins

All plugins listed [here](https://www.mapbox.com/mapbox.js/plugins/) are
supported:

* [turf](https://www.mapbox.com/mapbox.js/plugins/#turf)
* [directions](https://www.mapbox.com/mapbox.js/plugins/#mapbox-directions)
* [zoomslider](https://www.mapbox.com/mapbox.js/plugins/#leaflet-zoomslider)
* [pip](https://www.mapbox.com/mapbox.js/plugins/#point-in-polygon)
* [osm](https://www.mapbox.com/mapbox.js/plugins/#leaflet-osm)
* [omnivore](https://www.mapbox.com/mapbox.js/plugins/#leaflet-omnivore)
* [minimap](https://www.mapbox.com/mapbox.js/plugins/#leaflet-minimap)
* [markercluster](https://www.mapbox.com/mapbox.js/plugins/#leaflet-markercluster)
* [locate](https://www.mapbox.com/mapbox.js/plugins/#leaflet-locatecontrol)
* [label](https://www.mapbox.com/mapbox.js/plugins/#leaflet-label)
* [image](https://www.mapbox.com/mapbox.js/plugins/#leaflet-image)
* [heat](https://www.mapbox.com/mapbox.js/plugins/#leaflet-heat)
* [hash](https://www.mapbox.com/mapbox.js/plugins/#leaflet-hash)
* [geodesy](https://www.mapbox.com/mapbox.js/plugins/#leaflet-geodesy)
* [fullscreen](https://www.mapbox.com/mapbox.js/plugins/#leaflet-fullscreen)
* [draw](https://www.mapbox.com/mapbox.js/plugins/#leaflet-draw)
* [geojsonExtend](https://www.mapbox.com/mapbox.js/plugins/#static-map-from-geojson-with-geo-viewport)
* [geoViewport](https://www.mapbox.com/mapbox.js/plugins/#static-map-from-bounds-with-geo-viewport)
* [arc](https://www.mapbox.com/mapbox.js/plugins/#arcjs)

## Usage

Call `Mapbox.load()` in your client code. Use `Mapbox.loaded()` to check if it
finished loading. This function is reactive.

### API

#### `Mapbox.load(opts)`

    Mapbox.load({
        gl: boolean // optional
        plugins: list // optional
    })

* `opts` is optional.
* `gl`: if `true` [Mapbox GL](https://www.mapbox.com/mapbox-gl/) will be loaded

### Examples

    // Basic
    Meteor.startup(function(){
        Mapbox.load({
            plugins: ['minimap', 'markercluster']
        });
    });

    Deps.autorun(function () {
      if (Mapbox.loaded()) {
        L.mapbox.accessToken = MY_ACCESS_TOKEN;
        var map = L.mapbox.map('map', MY_MAP_ID);
      }
    });


    // Using a template's rendered callback
    Meteor.startup(function(){
        Mapbox.load();
    });

    Template.Map.rendered = function () {
        this.autorun(function () {
            if (Mapbox.loaded()) {
                L.mapbox.accessToken = TOKEN;
                var map = L.mapbox.map('map', MAP_ID);
            }
        });
    };
