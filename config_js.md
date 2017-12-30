# Configuration

Gulp merges config.js into config.default.js (config.default.js will be overwriten). **This is no deep merge**, you need to configure **complete** array or object like `nodeInfobox` or `supportedLocale`. You can use JS and functions to create new node details rows.

> **config.default.js** contains settings like `supportedLocale` or `maxAge`

> **config.js** contains communiy specific settings like stat images or `siteName` (and your overwrites of config.default.js)



## config.js

{% method %}
### dataPath (string/array)
`dataPath` needs a path/URL with meshviewer.js provided in an array. Don't forget the trailing slash!
Also, proxying the data through a webserver will allow brotli or deflat/gzip and thus will greatly reduce bandwidth consumption. `Access-Control-Allow-Origin: "*"` header should be added to allow local development.

{% sample lang="js" %}
Single data source
```js
'dataPath' : [
    'https://regensburg.freifunk.net/data/'
]
```

Multiple data sources
```js
'dataPath' : [
    'https://regensburg.freifunk.net/data/',
    'https://bremen.freifunk.net/data/'
]
```
{% endmethod %}


{% method %}
### siteName (string)
Change this to match your communities name. It will be used as HTML `<title>` and header.

{% sample lang='js' %}
```js
'siteName': 'Freifunk Regensburg'
```
{% endmethod %}

### mapLayers (List)

A list of objects describing map layers. Each object has at least `name`, `url` and `config` properties. [Example layers and configuration](http://leaflet-extras.github.io/leaflet-providers/preview/) (map against config.js).

[Layer provider list for meshviewer](/map-layers.md)

{% method %}
#### mode (string, optional)

Allows to load an additional style for a night mode or a similar use case. Possible are inline style or link. 
Inline avoids re-rendering and maybe issues with label-layer update. Important are class "css-mode mode-name" and media "not".

_Default is night.css inline in index.html_

{% sample lang='js' %}
```js
'mode': 'night'
```

`html/index.html`
```html
 <link rel="stylesheet" class="css-mode mode-name" media="not" href="mode-name.css">
```

or

```html
<style class="css-mode mode-name" media="not">
   <inline src="mode-name.css" />
</style>
```
{% endmethod %}


{% method %}
#### start (integer, optional)

Start a time range to put this mapLayer on first position.
{% sample lang='js' %}
```js
'start': 19
```
{% endmethod %}


{% method %}
#### end (integer, optional)

End a time range for first map. Stops sort this mapLayer.

{% sample lang='js' %}
```js
'end': 7
```
{% endmethod %}


{% method %}
### fixedCenter (array[array, array])

Choose a rectangle that must be displayed on the map. Set 2 Locations and everything between will displayed.

{% sample lang='js' %}
Examples for `fixedCenter`:

```js
'fixedCenter': [
  [
    49.3522,
    11.7752
  ],
  [
    48.7480,
    12.8917
  ]
],
```
{% endmethod %}


{% method %}
### nodeInfos (array, optional)

This option allows to show node statistics depending on following case-sensitive parameters:

- `name` header of statistics segment in infobox
- `href` absolute or relative URL to statistics image
- `image` `(required)` absolute or relative URL to image,
  can be the same like `href`
- `title` for the image

To insert current variables in either `href`, `image` or `title`
you can use the case-sensitive template string `{NODE_ID}`, `{NODE_NAME}`, `{LOCALE}` and `{TIME}` as cache-breaker.

In order to have statistics images available, you have to set up an instance of each [Prometheus](http://prometheus.io/) and [Grafana](http://grafana.org/).ve template string `{NODE_ID}`, `{NODE_NAME}`, `{LOCALE}` and `{TIME}` as cache-breaker.

{% sample lang='js' %}
Examples for `nodeInfos`:

```js
'nodeInfos': [
  { 
    'name': 'Clientstatistik',
    'href': 'stats/dashboard/db/node-byid?var-nodeid={NODE_ID}',
    'image': 'stats/render/dashboard-solo/db/node-byid?panelId=1&fullscreen&theme=light&width=600&height=300&var-nodeid={NODE_ID}&var-host={NODE_NAME}&_t={TIME}',
    'title': 'Knoten {NODE_ID}'
  },
  {
    'name': 'Uptime',
    'href': 'stats/dashboard/db/node-byid?var-nodeid={NODE_ID}',
    'image': 'stats/render/dashboard-solo/db/node-byid?panelId=2&fullscreen&theme=light&width=600&height=300&var-nodeid={NODE_ID}&_t={TIME}',
    'title': 'Knoten {NODE_ID}'
  }
]
```

In order to have statistics images available, you have to set up an instance of each [Prometheus](http://prometheus.io/) and [Grafana](http://grafana.org/).
{% endmethod %}


{% method %}
### globalInfos (array, optional)

This option allows to show global statistics on statistics page depending on following case-sensitive parameters:

- `name` header of statistics segment in infobox
- `href` absolute or relative URL to statistics image
- `image` `(required)` absolute or relative URL to image,
  can be the same like `href`
- `title` for the image

To insert locale or cache-breaker variable in either `href`, `image` or `title`
you can use the case-sensitive template strings `{LOCALE}` and `{TIME}` as cache-breaker.



{% sample lang='js' %}
Examples for `globalInfos` using Grafana server rendering:

```js
'globalInfos': [
  { 
    'name': 'Wochenstatistik',
    'href': 'stats/render/render/dashboard-solo/db/global?panelId=1&fullscreen&theme=light&width=600&height=300',
    'image': 'nodes/globalGraph.png',
    'title': 'Bild mit Wochenstatistik'
  }
]
```
{% endmethod %}


{% method %}
### linkInfos (array, optional)

This option allows to show link statistics depending on the following case-sensitive parameters:

- `name` header of statistics segment in infobox
- `href` absolute or relative URL to statistics image
- `image` `(required)` absolute or relative URL to image,
  can be the same like `href`
- `title` for the image

To insert the source or target variable in either `href`, `image` or `title`
you can use the case-sensitive template strings `{SOURCE_ID}`, `{TARGET_ID}`, `{SOURCE_NAME}`, `{TARGET_NAME}`, `{LOCALE}` and `{TIME}` as cache-breaker.

{% sample lang='js' %}
```js
'linkInfos': [
  {
    'name': 'Linkstatistik',
    'href': 'stats/dashboard/db/links?var-source={SOURCE_ID}&var-target={TARGET_ID}',
    'image': 'stats/render/dashboard-solo/db/links?panelId=1&fullscreen&theme=light&width=800&height=600&var-source={SOURCE_ID}&var-target={TARGET_ID}&_t={TIME}',
    'title': 'Bild mit Linkstatistik'
  }
]
```
{% endmethod %}


{% method %}
### siteNames (array, optional)

In this array name definitions for site statistics and node info can be saved. This requires one object for each site code. This object must contain:

- `site` the site code
- `name` the defined written name for this site code

If neither `siteNames` nor `showSites` are set, site statistics and node info won't be displayed.

{% sample lang='js' %}
Example for `siteNames`:

```js
  'siteNames': [
    {
      'site': 'ffrgb',
      'name': 'Regensburg'
    },
    {
      'site': 'ffrgb-dummy',
      'name': 'Regensburg Test'
    }
  ]
```
{% endmethod %}


## config.default.js

{% method %}
### reverseGeocodingApi (string)
Use a reverse proxy or own geocoding server for more data privacy and avoiding NoScript second domain. Use in location-picker.

{% sample lang='js' %}
```js
'reverseGeocodingApi': 'https://nominatim.openstreetmap.org/reverse'
```
{% endmethod %}


{% method %}
### maxAge (string)
Nodes being online for less than maxAge days are considered "new". Likewise,
nodes being offline for more than than maxAge days are considered "lost".

{% sample lang='js' %}
```js
'maxAge': 14
```
{% endmethod %}


{% method %}
### maxAgeAlert (integer)
Nodes being offline for more than than maxAge days are considered "lost".
Lost will be splitted in alert and lost.

{% sample lang='js' %}
```js
'maxAgeAlert': 3
```
{% endmethod %}


{% method %}
### nodeZoom (integer)
Max level to be applied by clicking a node or opening a node. Value `18` is a good default, so nearby buildings and streets should be visible.

{% sample lang='js' %}
```js
'nodeZoom': 18
```
{% endmethod %}


{% method %}
### labelZoom (integer)
Min. level for node labels shown on the map. Labels aren't shown in first zoom levels and every possible level labelZoom to maxZoom needs performance.

{% sample lang='js' %}
```js
'labelZoom': 13
```
{% endmethod %}


{% method %}
### clientZoom (integer)
Min. level to set starting layer for client dots on map.

{% sample lang='js' %}
```js
'clientZoom': 15
```
{% endmethod %}


{% method %}
### nodeAttr (array)
Remove or add node properties in detail view. Support `show` function in `utils/node` or properties from node (1 depth only)

{% sample lang='js' %}
```js
'nodeAttr': [
    // value can be a node attribute (1 depth) or a a function in utils/node with prefix show
    {
      'name': 'node.status',
      'value': 'Status'
    },
    {
      'name': 'node.gateway',
      'value': 'Gateway'
    },
    {
      'name': 'node.coordinates',
      'value': 'GeoURI'
    },
// Remove unwanted attributes    
//    {
//      'name': 'node.contact',
//      'value': 'owner'
//    },
    {
      'name': 'node.hardware',
      'value': 'model'
    },
    {
      'name': 'node.primaryMac',
      'value': 'mac'
    },
    {
      'name': 'node.firmware',
      'value': 'Firmware'
    },
    {
      'name': 'node.uptime',
      'value': 'Uptime'
    },
    {
      'name': 'node.firstSeen',
      'value': 'FirstSeen'
    },
    {
      'name': 'node.systemLoad',
      'value': 'Load'
    },
    {
      'name': 'node.ram',
      'value': 'RAM'
    },
    {
      'name': 'node.ipAddresses',
      'value': 'IPs'
    },
    {
      'name': 'node.update',
      'value': 'Autoupdate'
    },
    {
      'name': 'node.site',
      'value': 'Site'
    },
    {
      'name': 'node.clients',
      'value': 'Clients'
    }
  ]
```
{% endmethod %}


{% method %}
### supportedLocale (array)
Add supported locale (with matching language file in locales/*.js) and it will be matched against the browser language setting. Fallback is the first language in the array.

{% sample lang='js' %}
Example for `supportedLocale`:

```js
'supportedLocale': [
  'en',
  'de',
  'cz',
  'fr',
  'tr',
  'ru'
]
```
{% endmethod %}


{% method %}
### color (array)
Different color values for all canvas related settings and couldn't be done via SCSS.

{% endmethod %}


{% method %}
### cacheBreaker (string)
Will be replaced in every build to avoid missing or outdated language strings, because language.js isn't up to date.

_Fixed value (vy0zx)._
{% endmethod %}
