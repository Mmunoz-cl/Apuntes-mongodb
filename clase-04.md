## contar registros

```js
db.Productos.find().count()
```

## mostrar valores unicos
```js
db.Productos.distinct("precio")
```

## Busqueda de textos

```js
db.Productos.find({campo: /.*busqueda.*/ }) //que contenga

db.Productos.find({campo: /.*busqueda./ }) //que comience con

db.Productos.find({campo: /.busqueda.*/ }) //que termine con 
```

## Eliminacion de documentos
```js
db.Productos.deleteOne() // si no se pasa condicion borra el primer registro , si se le pasa borra la primera coincidencia

db.Productos.deleteMany() // si no se pasa condicion borra todo , si se le pasa borra todas las coincidencias
```