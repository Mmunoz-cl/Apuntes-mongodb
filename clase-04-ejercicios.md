
## 1.Listar registros de la coleccion "Productos" cuando la columna "nombre" del producto termine en "5" o (precio>=2000 y precio <=3000)

<details>
<summary>Ver Respuesta</summary>

```js
db.Productos.find({$or:[{producto: /5$/}, {$and:[{precio: {$gte: 2000}}, {precio: {$lte: 3000}}]}]})
```

</details>

## 2.Listar solo los atributos: id_producto, producto, cantidad de los registros de la coleccion "Productos".

<details>
<summary>Ver Respuesta</summary>

```js
db.Productos.find({},{id_producto:1, producto:1, cantidad:1})
```

</details>

## 3.Listar los registros y atributos: id_producto, nombre, cantidad, cuando la (cantidad >=30 y cantidad <=50) o precio <=1000.

<details>
<summary>Ver Respuesta</summary>

```js
db.Productos.find({$or:[{$and: [{cantidad: {$gte: 30}}, {cantidad: {$lte: 50}} ]}, {precio: {$lte: 1000}}]}, {id_producto:1, producto:1, cantidad:1})
```

</details>

## 4.Contar la cantidad de registros en donde el (precio >= 2000 y precio <= 3000)

<details>
<summary>Ver Respuesta</summary>

```js
db.Productos.find({$and: [{precio: {$gte: 2000}}, {precio: {$lte: 3000}}]}).count()
```

</details>

## 5.Listar registros en la coleccion "Productos", cuando la columna "Producto" del producto comience "Pr" y precio sea = 4000

<details>
<summary>Ver Respuesta</summary>

```js
db.Productos.find({$and: [{producto: /^Pr/}, {precio: 4000}]})
```

</details>

## 6.Mostrar valores unicos para el atributo cantidad de la coleccion

<details>
<summary>Ver Respuesta</summary>

```js
db.Productos.distinct("cantidad")
```

</details>

## 7.Eliminar registros en donde: precio sea mayor a 2000 y precio menor que 3000.

<details>
<summary>Ver Respuesta</summary>

```js
db.Productos.deleteMany({$and:[{precio: {$gt: 2000}}, {precio: {$lt: 3000}}]})
```

</details>

## 8.Eliminar registros en donde la cantidad se encuentre entre los valores 40 y 70

<details>
<summary>Ver Respuesta</summary>

```js
db.Productos.deleteMany({$and:[{cantidad: {$gte: 40}}, {cantidad: {$lte: 70}}]})
```

</details>