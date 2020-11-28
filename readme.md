# Roadnet Visualization

Playing around with OSM streetmaps generating network features

## Examples

### Dependencies
Load dependencies: 

```
import osmnx as ox
import networkx as nx
```

### Extract Graphs

#### From place name
Draw graph: 
```
G = ox.graph_from_place('Kapitolyo, Pasig, Philippines')
ox.plot_graph(G)
```

![Alt text](https://github.com/docligot/roadnet/blob/main/kapitolyo.png)


```
P = ox.graph_from_place('Cotabato City, Philippines')
ox.plot_graph(P)
```

![Alt text](https://github.com/docligot/roadnet/blob/main/cotabato.png)


#### From bounding box

```
A = ox.graph_from_bbox(14.59507018336878, 14.586083457806538, 120.9692932563976, 120.97993524101435, network_type='drive')
A_projected = ox.project_graph(A)
ox.plot_graph(A_projected)
```

![Alt text](https://github.com/docligot/roadnet/blob/main/intramuros.png)


### Extract Nodes and Edges

```
gdf_nodes, gdf_edges = ox.graph_to_gdfs(A)

gdf_nodes # get nodes
```

Node list: 

![Alt text](https://github.com/docligot/roadnet/blob/main/nodes.png)

```
gdf_edges # get edges
```


Edge list: 
![Alt text](https://github.com/docligot/roadnet/blob/main/edges.png)

#### Extract to CSV

```
gdf_nodes.to_csv('intramuros_graph.csv')
gdf_edges.to_csv('intramuros_streets.csv')

```

## References

* OSMNX: https://geoffboeing.com/2016/11/osmnx-python-street-networks/
* Stack Overflow: https://stackoverflow.com/questions/63464608/how-can-i-extract-road-networks-from-openstreet-map-with-python