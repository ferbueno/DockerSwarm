placement:
	constraints:
		node.id	Node ID	node.id == 2ivku8v2gvtg4 <-- Para sincronizar Percona MongoDB y algún otro servicio.
		node.hostname	Node hostname	node.hostname != node-2
		node.role	Node role	node.role == manager
		node.labels	user defined node labels	node.labels.security == high <-- Para sincronizar Percona MongoDB y algún otro servicio.
												node.id == data.node.id ????