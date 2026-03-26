## Crear Base de datos asignaturas inscritas
```
use asignaturas-inscritas
```

## Crear collection Alumnos
```js
db.createCollection("Alumnos")
```

## Insertar utilizando one
```js
db.Alumnos.insertOne({id_alumno : 001, 
                      nombre: "Luis", 
                      apellido: "Lopez", 
                      carrera: "Informatica", 
                      asignaturas: [{id_asignatura: "asig_0001", 
                                     asignatura: "Matematica"}, 
                                    {id_asignatura: "asig_0002", 
                                     asignatura: "Lenguaje"}] 
                    })
```

## Insertar utilizando many
```js
db.Alumnos.insertMany([
                        {id_alumno: "002", 
                        nombre: "Ana", 
                        apellido: "Jara", 
                        carrera: "Administracion", 
                        fecha_nacimiento: "2000-05-03", 
                        asignaturas: [{id_asignatura: "asig_0010", 
                                    asignatura: "Contabilidad"}]},
                        {id_alumno : "004", 
                        nombre: "Jose", 
                        apellido: "Aravena", 
                        asignaturas: [{id_asignatura: "asig_0011", 
                                    asignatura: "Administracion"},
                                    {id_asignatura: "asig_0012", 
                                    asignatura: "Finanzas" }]} 
                        ])
```
