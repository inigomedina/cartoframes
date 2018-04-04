## Cartography

Map creation in cartoframes happens through the `CartoContext.map` method. This method takes a list of map layers. The layers can be a `BaseMap`, table layer (`Layer`), or a query against data in the user's CARTO account (`QueryLayer`). Each of the layers is styled independently and appear on the map in the order listed.

### Base Maps

To create a map with only the `BaseMap`, do the following:

```python
from cartoframes import CartoContext, BaseMap
cc = CartoContext(
    base_url='your base url',
    api_key='your api key'
)
cc.map(layers=BaseMap())
```

To change the basemap style to CARTO's 'dark matter', pass the source keyword:

```python
cc.map(layers=BaseMap(source='dark'))
```

Remove labels with `labels=None` or put them in back with `labels='back'`.

### Single Layer Map

To add a data layer to your map, first find a table you wnat to visualize. Then use the following code to visualize this data:

```python
cc.map(layers=[
    BaseMap(),
    Layer('your table name')
])
```

### Multi Layer Map

To add several layers to your map, add them in the order you want them to display:


```python
cc.map(layers=[
    BaseMap(),
    Layer('biodiversity'),
    QueryLayer("SELECT * FROM table WHERE type != 'bird'")
])
```

### Style Size by Variable

To style by size variable, use the `size` keyword at the layer level for each layer passed. This only work for point data.

This sizes each point the same size (15 pixels wide).
```python
cc.map(layers=Layer('acadia_biodiversity', size=15))
```

To size by a variable, pass a column name instead of a number:

```python
cc.map(
    layers=Layer(
        'acadia_biodiversity',
        size='simpson_index'
    ))
```


### Style Color by Variable

Styling values by color is similar to styling by size but using the `color` keyword in the Layer object instead. Color by value works for points, lines, and polygons.

### Animated Map