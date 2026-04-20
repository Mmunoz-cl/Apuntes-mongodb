## Variables
```js
var valores1 = [1, 2, 3]
var valores2 = [4, 5, 6]

var usuario1 = {nombre: "juan", escala: valores2}

// Insertando registro almacenado en variable 
db.ejemplo_arreglo.insertOne(usuario1)
// Insertando registro con valores almacenados en variable
db.ejemplo_arreglo.insertOne({nombre: "maria",escala: valores1})

``` 

## Operaciones con arreglos
- Agregar un valor sin repetir ($addToSet)
```js
db.ejemplo_arreglo.updateMany({}, {$addToSet: { escala: 4 }})
```

- Agregar al final ($push)
```js
db.ejemplo_arreglo.updateMany({}, {$push: { escala: 4 }})
```

- Agregar multiples valores sin repetir ($each + $addToSet)
```js
db.ejemplo_arreglo.updateMany({}, {$addToSet: {escala: { $each: [5, 6] }}})
```

- Agregar y ordenar ($push + $each + $sort)
```js
db.ejemplo_arreglo.updateMany({}, {$push: {escala: {$each: [5, 6], $sort: 1}}}) 
// 1 ascendente, -1 descendente
```

## Eliminar elemento de un arreglo ($pull)
```js
db.ejemplo_arreglo.updateMany({}, {$pull: { escala: 4 }})
```

## Consultas con arreglos
- Mostrar campo arreglo
```js
db.ejemplo_arreglo.find({}, {_id: 0, escala: 1})
```

## Obtener cantidad determinada ($slice)

Ultimos 2 elementos:
```js
db.ejemplo_arreglo.find({}, {_id: 0, nombre: 1, escala: { $slice: -2 }})
```

## Definir intervalo ($slice)

Desde posicion 1, devuelve 3 elementos:
```js
db.ejemplo_arreglo.find({}, {escala: { $slice: [1, 3] }})
```

- Buscar multiples valores en arreglo ($all)

```js
db.ejemplo_arreglo.find({escala: { $all: [6, 2] }}, {_id: 0, escala: 1})
// Retorna documentos donde el arreglo contiene ambos valores.
```

## Actualizar 
```js
db.productos.updateMany({ precio: { $gte: 2500, $lte: 4000 }},
                        { $set: { categoria: "medio" }})
```

# Notas importantes
* $addToSet → evita duplicados
* $push → permite duplicados
* $each → agrega multiples valores
* $each → se usa junto a $push o $addToSet
* $slice → limita resultados del arreglo
* $all → busca multiples coincidencias en arrays
* $pull → elimina elementos especificos