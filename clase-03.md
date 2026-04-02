## 1.Listar el campo Producto para todos los registros

```js
db.Productos.find({}, {producto:1})
```
## 2.Listar el campo id_producto , producto , precio para todos los registros

```js
db.Productos.find({}, {id_producto:1, producto:1, precio:1})
```

## 3.Listar todos los campos para los registros cuyo precio sea menor a 2500
```js
db.Productos.find({precio : {$lte : 2500}})
```
## 4.Listar los campos id_producto, producto, precio para los registros cuya cantidad sea distinto a 30
```js
db.Productos.find({cantidad : {$ne : 30}}, {id_producto:1, producto:1, precio:1})
```
## 5.Listar todos los campos para los registros mayor o igual a 2500 y cantidad menor o igual a 40
```js
db.Productos.find({$and: [{precio: {$gte : 2500}}, {cantidad: {$lte: 40}}]})
```