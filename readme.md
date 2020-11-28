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
	y	x	osmid	highway	geometry
21638762	14.593700	120.974169	21638762	NaN	POINT (120.97417 14.59370)
21638763	14.593708	120.974958	21638763	NaN	POINT (120.97496 14.59371)
21638765	14.594297	120.974956	21638765	NaN	POINT (120.97496 14.59430)
21638771	14.594657	120.977928	21638771	milestone	POINT (120.97793 14.59466)
21638777	14.587911	120.976478	21638777	NaN	POINT (120.97648 14.58791)
...	...	...	...	...	...
6633789015	14.589954	120.978502	6633789015	NaN	POINT (120.97850 14.58995)
7555626796	14.588874	120.971046	7555626796	NaN	POINT (120.97105 14.58887)
7555626807	14.588436	120.970587	7555626807	NaN	POINT (120.97059 14.58844)
7555626817	14.587646	120.969758	7555626817	NaN	POINT (120.96976 14.58765)
7555626818	14.589438	120.971638	7555626818	NaN	POINT (120.97164 14.58944)

```
gdf_edges # get edges
```

Edge list: 
osmid	lanes	name	highway	maxspeed	oneway	length	geometry	ref	u	v	key
0	158627310	2	Solana Street	unclassified	30	False	43.606	LINESTRING (120.97417 14.59370, 120.97446 14.5...	NaN	21638762	163734761	0
1	161306392	4	Andres Soriano Avenue	secondary	40	False	65.367	LINESTRING (120.97417 14.59370, 120.97419 14.5...	NaN	21638762	703530319	0
2	34363668	4	A. Soriano Avenue	secondary	40	False	161.689	LINESTRING (120.97417 14.59370, 120.97405 14.5...	NaN	21638762	3388766875	0
3	161414175	2	NaN	unclassified	40	False	8.291	LINESTRING (120.97496 14.59371, 120.97496 14.5...	NaN	21638763	1055759279	0
4	331769752	3	Muralla Street	unclassified	40	True	17.676	LINESTRING (120.97496 14.59371, 120.97479 14.5...	NaN	21638763	997427805	0
...	...	...	...	...	...	...	...	...	...	...	...	...
327	807971933	1	16th Street	tertiary	35	True	125.145	LINESTRING (120.97059 14.58844, 120.96980 14.5...	NaN	7555626807	7555626817	0
328	16176619	NaN	A.C. Delgado Street	tertiary	35	False	4.625	LINESTRING (120.96976 14.58765, 120.96979 14.5...	NaN	7555626817	163749626	0
329	16176619	NaN	A.C. Delgado Street	tertiary	35	False	57.373	LINESTRING (120.96976 14.58765, 120.96972 14.5...	NaN	7555626817	163749521	0
330	4075790	4	Bonifacio Drive	trunk	60	True	4.506	LINESTRING (120.97164 14.58944, 120.97166 14.5...	120	7555626818	616061273	0
331	807971933	1	16th Street	tertiary	35	True	89.348	LINESTRING (120.97164 14.58944, 120.97105 14.5...	NaN	7555626818	7555626796	0

Extract to CSV:

```
gdf_nodes.to_csv('intramuros_graph.csv')
gdf_edges.to_csv('intramuros_streets.csv')

```