# No SQL Query Implementation

## 1 User Posts Query:
### Original query 
 Retrieve the most popular active posts and display their title and like count


```
db.posts
  .find({ status: "active" }, { title: 1, likes: 1 })
  .sort({ likes: -1 });

```
### Mejoras:

Indexación: 

* Crear un índice compuesto en { status: 1, likes: -1 } optimiza el rendimiento porque ayuda a filtrar primero por status y después ordenar rápido por likes.

Esquema:
* Si consultamos posts populares con frecuencia, podríamos considerar añadir un campo isPopular que se actualice periódicamente, lo que evitaría hacer el sort sobre likes en tiempo real.

## 2 User Data Aggregation: 
Summarize the number of active users by location.

### Original query


```
db.users.aggregate([
  { $match: { status: "active" } },
  { $group: { _id: "$location", totalUsers: { $sum: 1 } } },
]);

```
### Mejoras:


Indexación:
* Un índice en { status: 1, location: 1 } permite que se filtre más rápido los usuarios activos y agrupe por location de manera eficiente.

Esquema:
* Si se consulta frecuentemente el número de usuarios activos por location, se podria almacenar este conteo en un campo activeUserCount dentro de cada location y actualizarlo periódicamente.