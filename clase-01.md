## Conexion 

```
mongosh
```

## Listar bases

```
show dbs
```

## Cambiar a una base de datos o crearla si no existe

```
use nombrebase
```

## Crear coleccion

```js
db.createCollection("nombredecoleccion")
```

## Mostrar colecciones

```
show collections
```

## Insertar Registro

```js
db.insertOne({clave : "valor"})
```

```js
db.insertMany([{clave1: "valor"}, {clave2: "valor"}])
```

## Borrar coleccion
```js
db.nombredelacoleccion.drop()
```

## Borrar Base
```js
db.dropDatabase()
```