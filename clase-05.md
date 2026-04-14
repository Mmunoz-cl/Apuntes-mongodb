## Actualizar registros
``` js
db.Productos.updateOne({id_producto: 2}, {$set: {precio: 5000}})
db.Productos.updateMany({$or:[{id_producto: 2}, {id_producto: 7}]}, {$set:{precio:5000}})
```

## Busqueda en documentos embebidos

```js
db.Productos.find({'detalle.talla':"L"})

db.Productos.find({$and: [{cantidad: 20}, {'detalle.color' : "Negro"}]})

```