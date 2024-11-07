# Provided SQL Queries for Optimization

## 1 Orders query
### Original query


```
SELECT Orders.OrderID, SUM(OrderDetails.Quantity * OrderDetails.UnitPrice) AS TotalPrice
FROM Orders
JOIN OrderDetails ON Orders.OrderID = OrderDetails.OrderID
WHERE OrderDetails.Quantity > 10
GROUP BY Orders.OrderID;

```
### Mejoras:

	1.	Indexación:
    	•	Poner un índice en OrderDetails.OrderID para acelerar el JOIN.
	    •	Otro índice en OrderDetails.Quantity ayudaria a filtrar más rápido por el WHERE.
	2.	JOIN optimizado:
	    •	Usar INNER JOIN explícitamente, porque aquí solo queremos las filas que están en ambas tablas (filtrado por Quantity > 10), lo que mejora el rendimiento.
###
```
SELECT Orders.OrderID, SUM(OrderDetails.Quantity * OrderDetails.UnitPrice) AS TotalPrice
FROM Orders
INNER JOIN OrderDetails ON Orders.OrderID = OrderDetails.OrderID
WHERE OrderDetails.Quantity > 10
GROUP BY Orders.OrderID;

```

## 2 Customer Query
```
SELECT CustomerName FROM Customers WHERE City = 'London' ORDER BY CustomerName;
```
### Mejoras
	1.	Indexación:
	* Crear un índice compuesto en City y CustomerName ayuda a filtrar y ordenar más rápido porque la base de datos accede directamente a lo que necesita.