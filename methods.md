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
Change this to match your communities name. It will be used as HTML `<title>` and header.

{% sample lang="json" %}
```json
"siteName": "Freifunk Regensburg"
```
{% endmethod %}


