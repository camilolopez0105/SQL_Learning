DISTINCT selecciona valores unicos
SELECT se puede usar en varias columnas separando con , (CustomerName, City, Country)
(*) Es para seleccionar todo
LIMIT 3; (Se usa para limitar y evitar sacar todo)
TOP 3, se usa en SQL Server o SQLite
SELECT * FROM Products;
SELECT	 ProductName, Price FROM Products;
select * from Suppliers;
select SupplierName, City, Country from suppliers;
select distinct Country from suppliers;
SELECT top 5 CustomerName FROM Customers;
SELECT top 2 shippername, phone FROM Shippers;
SELECT distinct country FROM Suppliers;
SELECT * FROM Products Where Price > 20
SELECT * FROM Customers WHERE Country = 'Mexico'
SELECT * FROM Customers WHERE Country = 'Mexico' AND PostalCode = 05021
SELECT * FROM Customers WHERE Country = 'Spain' OR Country = 'Germany'
SELECT * FROM Products WHERE CategoryID = 1 AND (Price <10 OR Price >40)
SELECT * FROM Products WHERE Price = 10
SELECT * FROM Products WHERE Price >= 50
SELECT * FROM Customers WHERE Country = 'UK'
SELECT * FROM Suppliers WHERE Country != 'USA'
SELECT * FROM Products WHERE CategoryID = 2 AND Price < 20
SELECT * FROM Customers WHERE Country = 'UK' AND City = 'London'
SELECT * FROM Employees WHERE FirstName = 'Laura' OR FirstName = 'Nancy'
SELECT * FROM Products WHERE CategoryID = 3 OR CategoryID = 4
SELECT * FROM Customers WHERE Country = 'Germany' AND (City = 'Berlin' OR City = 'Aachen')
SELECT * FROM Products WHERE (CategoryID = 1 OR CategoryID = 2) AND Price >= 50
SELECT * FROM Customers WHERE Country IN ('Spain','Germany','France')
SELECT * FROM Products WHERE Price BETWEEN 10 AND 20
SELECT * FROM Customers WHERE ContactName LIKE 'Ma%'
SELECT * FROM Customers WHERE Country IN('France','Spain','Italy')
SELECT * FROM Customers Where City != 'London' AND City != 'Seattle'
SELECT * FROM Customers Where City NOT IN ('London','Seattle')
SELECT * FROM Orders WHERE EmployeeID BETWEEN 2 AND 4
SELECT * FROM Customers WHERE (ContactName LIKE 'A%') AND (Country = 'USA' OR Country = 'UK')
SELECT * FROM Employees Where Notes LIKE '%psychology%'
SELECT * FROM Customers ORDER BY Country
SELECT * FROM Customers ORDER BY Country DESC
SELECT * FROM Products ORDER BY Price DESC
SELECT * FROM Customers ORDER BY Country ASC, City DESC
SELECT
 ProductName AS Nombre_Producto,
    Price AS Precio
FROM Products;
COUNT (*) -> Cuenta filas
COUNT (columna) -> cuenta valores no nulos en esa columna
SELECT
 Country,
    COUNT(*) AS Numero_Clientes
FROM Customers
Group BY Country
ORDER BY Numero_Clientes DESC;
WHERE Filtra filas antes de agrupar
HAVING Filtra grupos despues de agrupar
1. ¿Cuántos productos hay en total?
SELECT COUNT(*) AS Total_Productos
FROM Products;
2. ¿Cuál es el precio medio de los productos?
SELECT AVG(Price) AS Precio_Medio
FROM Products;
3. ¿Cuál es el producto más caro?
SELECT MAX(Price) AS Precio_Maximo 
FROM Products;
SELECT TOP 1 *
FROM Products
ORDER BY Price DESC;
4. ¿Cuál es el producto más barato?
SELECT MIN(Price) AS Precio_Minimo 
FROM Products;
SELECT TOP 1 *
FROM Products
ORDER BY Price;
5. ¿Cuántos clientes hay por país?
SELECT Country, COUNT (*) AS Total_Clientes
FROM Customers
GROUP BY Country;
6. ¿Cuántos proveedores hay por país?
SELECT Country, COUNT (*) AS Total_Proveedores
FROM Suppliers
GROUP BY Country;
7. ¿Cuántos productos hay por categoría?
SELECT CategoryID, COUNT(*) AS Total_Productos
FROM Products
GROUP BY CategoryID
8. Muestra solo las categorías que tengan más de 10 productos.
SELECT CategoryID, COUNT(*) AS Total_Productos
FROM Products
Group BY CategoryID
HAVING COUNT(*) > 10
9. Calcula el precio medio por categoría.
SELECT CategoryID, AVG(Price) AS Precio_Medio
FROM Products
GROUP BY CategoryID
10. Muestra los países con más de 3 clientes, ordenados de mayor a menor.
SELECT Country, COUNT(*) AS Total_Clientes
FROM Customers
GROUP BY Country
HAVING COUNt(*) > 3
ORDER BY Total_Clientes DESC;
11. SELECT
 Products.ProductName,
    Categories.CategoryName,
    Products.Price
FROM Products
INNER JOIN Categories
 ON Products.categoryID = Categories.categoryID;
-- 1
SELECT
  p.ProductName,
  c.CategoryName
FROM Products AS p
INNER JOIN Categories AS c
  ON p.CategoryID = c.CategoryID;

-- 2
SELECT
  p.ProductName,
  p.Price,
  s.SupplierName
FROM Products AS p
INNER JOIN Suppliers AS s
  ON p.SupplierID = s.SupplierID;

-- 3
SELECT
  o.OrderID,
  e.FirstName,
  e.LastName,
  o.OrderDate
FROM Orders AS o
INNER JOIN Employees AS e
  ON o.EmployeeID = e.EmployeeID;

-- 4
SELECT
  e.FirstName,
  e.LastName,
  COUNT(*) AS Total_Pedidos
FROM Orders AS o
INNER JOIN Employees AS e
  ON o.EmployeeID = e.EmployeeID
GROUP BY e.FirstName, e.LastName
ORDER BY Total_Pedidos DESC;
# Reto final: empleado del mes

## Contexto

La empresa quiere analizar el rendimiento de sus empleados. Necesita saber cuántos pedidos ha gestionado cada uno.

## Enunciado

Muestra:

- Nombre del empleado.
- Apellido del empleado.
- Total de pedidos gestionados.

Ordena el resultado de mayor a menor número de pedidos.
SELECT e.EmployeeID, e.FirstName, e.LastName, COUNT(*) as num_orders
FROM Employees e
INNER JOIN Orders o ON e.EmployeeID = o.EmployeeID
GROUP BY e.EmployeeID, e.FirstName, e.LastName
Order by num_orders DESC

Este bloque es de ejercicios extra por si quereis practicar:
## Extra A: exploración rápida

1. Muestra los 3 primeros productos.
2. Muestra los 10 primeros clientes.
3. Muestra todas las ciudades distintas de clientes.
4. Muestra todos los países distintos de proveedores.
5. Muestra `ProductName`, `Unit` y `Price` de todos los productos.
 ## Extra B: filtros

1. Productos con precio mayor o igual a 30.
2. Productos con precio menor o igual a 5.
3. Clientes de `Germany`.
4. Clientes que no sean de `Germany`.
5. Clientes cuyo nombre contenga `Restaurant`.
6. Proveedores cuyo teléfono contenga `555`.
7. Productos de categoría 4 o 5.
8. Productos cuyo precio no esté entre 10 y 50.
## Extra C: ordenación y ranking

1. Top 5 productos más caros.
2. Top 5 productos más baratos.
3. Clientes ordenados por país descendente.
4. Productos de la categoría 1 ordenados por precio descendente.
5. Proveedores de `USA` ordenados por ciudad.
## Extra D: agregaciones

1. Número total de clientes.
2. Número total de proveedores.
3. Precio medio de productos de la categoría 1.
4. Precio máximo de productos de la categoría 2.
5. Número de clientes por ciudad.
6. Número de pedidos por empleado.
7. Número de pedidos por transportista.
8. Países con al menos 5 clientes.
## Extra E: `JOIN`

1. Producto + categoría.
2. Producto + proveedor.
3. Pedido + empleado.
4. Pedido + transportista.
5. Producto + categoría + proveedor.
6. Cantidad total de productos por categoría, mostrando el nombre de categoría.
# Reto final extendido: mini análisis de negocio

## Contexto

Northwind quiere una primera foto de negocio para preparar un dashboard.

## Entregables

1. Top 10 productos más caros.
2. Número de clientes por país.
3. Países con más de 3 clientes.
4. Precio medio de productos por categoría.
5. Nombre de producto, categoría y proveedor.
6. Número de pedidos por empleado.
7. Número de pedidos por transportista.
8. Categoría con más productos.