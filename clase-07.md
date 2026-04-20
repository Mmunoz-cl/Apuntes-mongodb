# Aggregation
- Promedio total de precios
```js
db.productos.aggregate([{$group: {_id: null, promedio: { $avg: "$precio" }}}])

/*
$group → agrupa documentos
_id: null → todos los documentos en un solo grupo
$avg → calcula el promedio del campo precio
Resultado: un solo documento con el promedio total
*/
```


- Maximo precio por categoría
```js
db.productos.aggregate([{ $group: {_id: "$categoria", max: { $max: "$precio" }}}])

/*
Agrupa por categoria
$max → obtiene el precio más alto por categoria
*/
```

- Maximo y minimo por categoría
```js
db.productos.aggregate([
  {
    $group: {
      _id: "$categoria",
      max: { $max: "$precio" },
      min: { $min: "$precio" }
    }
  }
])

/*
Agrupa por categoria
Calcula el precio maximo y minimo
*/
```

## Suma de valores ($sum)
* Suma total
```js
db.productos.aggregate([{$group: {_id: null, total: { $sum: "$precio" }}}])

// Suma todos los precios
```

* Suma por categoría
```js
db.productos.aggregate([{ $group: {_id: "$categoria", total: { $sum: "$precio" }}}])

// Total de precios por categoria
```

* Suma de cantidades
```js
db.productos.aggregate([{$group: {_id: "$categoria", total_cantidad: { $sum: "$cantidad" }}}])

// Total de unidades por categoria
```

- Contar documentos
```js
db.productos.aggregate([{ $group: {_id: "$categoria", cantidad_productos: { $sum: 1 }}}])

// Cuenta documentos por categoria
```

## Promedios + filtro
```js
db.productos.aggregate([{ $group: {_id: "$categoria", promedio_precio: { $avg: "$precio" },
                                                      promedio_cantidad: { $avg: "$cantidad"}}},
                        { $match: {promedio_cantidad: { $gt: 5 }}}])
/*
Paso a paso
$group
Agrupa por categoria
Calcula promedios
$match
Filtra resultados
Solo deja categorias con promedio de cantidad > 5

Orden del pipeline (IMPORTANTE)
$group → $match

$match va después porque usa campos calculados
*/
```

## Notas importantes
* aggregate() → usa un arreglo []
* $group → agrupa documentos
* _id → define el criterio de agrupacion
* $avg → promedio
* $max → valor maximo
* $min → valor minimo
* $sum → suma
* $match → filtra resultados

## Conclusion
Aggregation funciona como una secuencia de pasos (pipeline):

1. Agrupar ($group)
2. Filtrar ($match)
3. (Opcional) transformar / ordenar