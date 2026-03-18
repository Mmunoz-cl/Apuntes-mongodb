## Conexion 

```
mongosh
```

## Listar bases

```
show dbs
```

## Cambiar o crear base de datos

```
use nombrebase
```

## Crear coleccion

```js
db.createCollection("nombredecoleccion")
```

## Mostrar coleccion

```
show collection
```

## Insertar Registro

```js
db.insertOne({clave : "valor"})
```

```js
db.inserMany({clave1: "valor"}, {clave2: "valor"})
```