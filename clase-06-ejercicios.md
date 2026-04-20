1. actualizar los registros que ciorrespondan a valores de precio entre 2500 y 4000
iniciando su categoria = 'lacteos' , para el resto categoria = ' fruta'

    * Primero agregar categoria lacteos segun condicion:
    ```js
    db.productos.updateMany({$and: [{precio: {$gte: 2500}},{precio: {$lte: 4000}}]},
                            {$set: {categoria: "lacteos"}})
    ```

    * Luego fruta para el resto:
    ```js
    db.productos.updateMany({$or: [{precio: {$lt: 2500}},{precio: {$gt: 4000}}]},
                            {$set: {categoria: "fruta"}})
    ```

2. para las categorias igual a fruta indicar los siguientes caracteristicas en un sub documento

- pais_origen: "?"
- fecha_elaboracion: "?"
- fecha_vencimiento: "?"

    ```js
    db.productos.updateMany({categoria: "fruta"},
                            {$set: {caracteristicas: {pais_origen: "francia", 
                                    fecha_elaboracion: "12-04-2026",
                                    fecha_vencimiento: "12-08-2026"}}})
    ```
para el caso de los productos categoria lacteos :

- fecha_elaboracion: ?
- fecha_vencimiento: ?

```js
db.productos.updateMany({categoria: "lacteos"},
                        {$set: {caracteristicas: { 
                                fecha_elaboracion: "12-04-2026",
                                fecha_vencimiento: "12-08-2026"}}})
```

3. agregar un nuevo atributo para todos los registros llamados "envase" 
En donde el producto 1 y 2 , tendran los valores de tipo arreglo[100,150] en su atributo envase

* Primero crear atributo envase para todos los registros:
```js
db.productos.updateMany({},{$set: {envase : []}})
```

* Luego insertar arreglo a productos 1 y 2
```js
db.productos.updateMany({nombre: {$in: ["Prod_1", "Prod_2"]}},
                        {$addToSet: { envase: {$each: [100,150]}}})
```

4. para el subdocumento "caracteristica" agregar el atributo "tipo" = "en polvo" para
el id_producto : 5, para el 3 y 4 sera "liquido"

* En Polvo:
```js
db.productos.updateOne({id_producto: 5},{$set: {'caracteristicas.tipo': "En polvo"}})
```
* Liquido
```js
db.productos.updateMany({id_producto: {$in: [3,4]}},
                        {$set: {'caracteristicas.tipo': "Liquido"}})
```

5. para los registros cuya cantidad sea (20 o 30) o precio = 4000; agregar la columna
color_envase que trandra el valor igual a cafe

```js
db.productos.updateMany({$or: [{cantidad: {$in: [20,30]}},{precio: 4000}]},
                        {$set: {color_envase: "cafe"}})
```

6. listar los registros en donde el envase contenga el valor: 100 o el atributo tipo del subdocumento sea igual a "polvo"
```js
db.productos.find({$or: [{envase: 100},{'caracteristicas.tipo' : "En polvo"}]})
```


7. agregar a la columna envase lo siguiente : 
cuando las cantidades sean 20 y 40 , debe contener [100,200,300], para los registros que tengan cantidad 10,30,50 o que en atributo tipo el subdocumento = liquido, debe contener 
[50, 150, 150]

* Agregando los valores [100,200,300] para registros con cantidad 20 o 40
```js
db.productos.updateMany({cantidad: {$in: [20, 40]}}, {$addToSet: {envase: {$each: [100,200,300]}}})
```

* Agregando los valores [50,150,150] para registros con cantidad 10 o 30 o 50
```js
db.productos.updateMany({$or:[{cantidad: {$in: [10,30,50]}},{'caracteristicas.tipo' : "Liquido"}]}, 
                        {$addToSet: {envase: {$each: [50,150,150]}}})
```
