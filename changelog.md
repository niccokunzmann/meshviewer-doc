# Changelog

## 10.0.0

* Performance improvements (critical path, avoid blocking code)
* Replaced router - including language, mode, node, link, location
* Leaflet upgraded to v1 - faster on mobile
* Forcegraph rewrite with d3.js v4
* Map layer modes \(Allow to set a default layer based on time combined with a stylesheet\)
* Automatic updates for selected node or list \(incl. image stats cache-breaker\)
* Node filter
* Zoom level for clicking on a node \(`nodeZoom`\) is definable independently from the maximum zoom level 22
* Formatted Code
* Translation support - Help to improve or add languages at [Online translation platform](https://poeditor.com/join/project/VZBjPNNic9)
  * Currently available: en, de, fr, cz, tk & ru
* Gulp inline for some css and js - fewer requests and instant load indicator
* Icon font with needed icons only
* Switch to Gulp \(Tested with Node.js 6 LTS, 8 on Linux, OSX & W\*\*\)
  * css and some js moved inline
* Yarn in favour of bower
  * Load only moment.js without languages \(Languages are included in translations\)
  * unneeded components removed \(es6-shim, tablesort, numeraljs, leaflet-providers, leaflet-label jshashes, chroma-js\)
* RBush v2 - performance boost in last versions \(positions, labels and clients on the map\)
* Ruby dependency removed
* FixedCenter is required
* Sass-lint, scss and variables rewritten for easy customizations/adjustments
* Cross browser/device support improved \(THX@BrowserStack\)
* Yarn package manager in favour of npm
* Configurable reverse geocoding server
* Split clients into 2,4, 5Ghz and others
* Show nexthop and gateways \(IPv4/IPv6\)
* Dynamic node detail attributes
* Config inheritance and functions
* Dynamic map center (sidebar toggle)
* Show connection type (icon)
^ Accessibility improvements
* Few Internet Explorer 11 fixes
* Necessary polyfills - no overhead
* **Switch to meshviewer.json - less depth, new informations**
* [A lot more in the commit history](https://github.com/ffrgb/meshviewer/commits/develop)



