# Configuration

{% method %}
### dataPath (string/array)
`dataPath` can be either a string containing the address of a Nodes.json v2 compatible backend (e.g. ffmap backend) or an array containing multiple addresses.
Don't forget the trailing slash!
Also, proxying the data through a webserver will allow GZip and thus will greatly reduce bandwidth consumption.
It may help with firewall problems too.

{% sample lang="json" %}
Sinple data source
```json
dataPath : "https://regensburg.freifunk.net/data/"
```

Multiple data sources
```json
dataPath : [
    "https://regensburg.freifunk.net/data/", 
    "https://nominatim.openstreetmap.org/reverse"
]
```
{% endmethod %}


{% method %}
### siteName (string)
Change this to match your communities name. It will be used as HTML `<title>` and header.

{% sample lang="json" %}
```json
"siteName": "Freifunk Regensburg"
```
{% endmethod %}


{% method %}
### maxAge (string)
Nodes being online for less than maxAge days are considered "new". Likewise,
nodes being offline for more than than maxAge days are considered "lost".

{% sample lang="json" %}
```json
"siteName": "Freifunk Regensburg"
```
{% endmethod %}


{% method %}
### maxAgeAlert (integer)

Nodes being offline for more than than maxAge days are considered "lost".
Lost will be splitted in alert and lost.
{% endmethod %}


{% method %}
### nodeZoom (integer)

Max level to be applied by clicking a node or opening a node. Value `18` is a good default, so nearby buildings and streets should be visible.
{% endmethod %}


{% method %}
### labelZoom (integer)

Min. level for node labels shown on the map. Labels aren't shown in first zoom levels and need performance.
{% endmethod %}


{% method %}
### clientZoom (integer)

Min. level to set starting layer for client dots on map.
{% endmethod %}


{% method %}
### nodeInfobox

#### contact (bool, optional)

Setting this to `false` will hide contact information for nodes.

#### hardwareUsage (bool, optional)

Setting this to `false` will hide bars of memory usage and load avg for nodes.
{% endmethod %}


{% method %}
### mapLayers (List)

A list of objects describing map layers. Each object has at least `name`, `url` and `config` properties. [Example layers and configuration](http://leaflet-extras.github.io/leaflet-providers/preview/) (map against config.json).

#### mode (string, optional)

Allows to load a additional style for a night mode or similar use case. Possible are inline style or link. 
Inline avoids re-rendering and maybe issues with label-layer update. Important are class "css-mode mode-name" and media "not".

_Default is night.css inline in index.html_

```html
 <link rel="stylesheet" class="css-mode mode-name" media="not" href="mode-name.css">
```

or

```html
<style class="css-mode mode-name" media="not">
   <inline src="mode-name.css" />
</style>
```

#### start (integer, optional)

Start a time range to put this mapLayer on first position.

#### end (integer, optional)

End a time range for first map. Stops sort this mapLayer.
{% endmethod %}


{% method %}
### fixedCenter (array[array, array])

Choose a rectangle that must be displayed on the map. Set 2 Locations and everything between will displayed.

{% sample lang="json" %}
Examples for `fixedCenter`:

```json
// Set a visible frame
"fixedCenter": [
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

Examples for `nodeInfos`:

```json
"nodeInfos": [
  { 
    "name": "Clientstatistik",
    "href": "stats/dashboard/db/node-byid?var-nodeid={NODE_ID}",
    "image": "stats/render/dashboard-solo/db/node-byid?panelId=1&fullscreen&theme=light&width=600&height=300&var-nodeid={NODE_ID}&var-host={NODE_NAME}&_t={TIME}",
    "title": "Knoten {NODE_ID}"
  },
  {
    "name": "Uptime",
    "href": "stats/dashboard/db/node-byid?var-nodeid={NODE_ID}",
    "image": "stats/render/dashboard-solo/db/node-byid?panelId=2&fullscreen&theme=light&width=600&height=300&var-nodeid={NODE_ID}&_t={TIME}",
    "title": "Knoten {NODE_ID}"
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

In contrast to `nodeInfos` there is no template substitution in  `href`, `image` or `title`.

Examples for `globalInfos` using Grafana server rendering:
{% sample lang="json" %}
```json
"globalInfos": [
  { 
    "name": "Wochenstatistik",
    "href": "stats/render/render/dashboard-solo/db/global?panelId=1&fullscreen&theme=light&width=600&height=300",
    "image": "nodes/globalGraph.png",
    "title": "Bild mit Wochenstatistik"
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

{% sample lang="json" %}
```json
"linkInfos": [
  {
    "name": "Linkstatistik",
    "href": "stats/dashboard/db/links?var-source={SOURCE_ID}&var-target={TARGET_ID}",
    "image": "stats/render/dashboard-solo/db/links?panelId=1&fullscreen&theme=light&width=800&height=600&var-source={SOURCE_ID}&var-target={TARGET_ID}&_t={TIME}",
    "title": "Bild mit Linkstatistik"
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

{% sample lang="json" %}
Example for `siteNames`:

```json
  "siteNames": [
    {
      "site": "ffrgb",
      "name": "Regensburg"
    },
    {
      "site": "ffrgb-dummy",
      "name": "Regensburg Test"
    }
  ]
```
{% endmethod %}


{% method %}
### supportedLocale (array)

Add supported locale (with matching language file in locales/*.json) and it will be matched against the browser language setting. Fallback is the first language in the array.

{% sample lang="json" %}
Example for `supportedLocale`:

```json
"supportedLocale": [
  "en",
  "de",
  "fr"
]
```
{% endmethod %}


{% method %}
### cacheBreaker (string)

Will be replaced in every build to avoid missing or outdated language strings, because language.json isn't up to date.

_Fixed value (y0z)._
{% endmethod %}