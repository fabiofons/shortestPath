# ShortestPath
```javascript
function Node(name) {
  this.name = name;
  this.refs = [];
}

// funcion para crear los nodos
function shortestPath(matrix , origin, dest) {
  const numNodes = matrix.length;
  let nodes = []; // nodes = [0, 1, 2, 3]
  for(let i = 0; i < numNodes; i++) {
    nodes[`${i}`] = new Node(i);
  }

  //crea las relaciones
  for (let row = 0; row < matrix.length; row++) {
    for (let col = 0; col < matrix.length; col++) {
      if (row !== col && matrix[row][col] > 0) {
        const node = nodes[col];
        const weight = matrix[row][col];
        nodes[row].refs.push([node, weight]);
      }
    }
  }
  return shortestPathRec(nodes[origin], nodes[dest]);
}

function shortestPathRec(origin, dest) {
  if(origin === dest) return 0;
  // creamos el arreglo de los diferentes caminos.
  let costs = [];
  origin.refs.forEach(function(ref) {
    let cost = shortestPathRec(ref[0], dest);
    if (cost !== -1) {
      costs.push(cost + ref[1]);
    }
  });

  return costs.length === 0 ? -1 : Math.min(...costs);
}
```
