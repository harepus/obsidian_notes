Skriv en spørring over Northwind-databasen som:
1. Finner navn på alle kunder fra London
```sql
SELECT company_name, contact_name
FROM customers
WHERE city LIKE 'London';
```
customers: company_name

2. Finner lasten (i tonn) for alle bestillinger som er sendt med skipene Around the Horn og Ernst Handel
```sql
SELECT (freight /1000) AS freight_in_tons
FROM orders 
WHERE ship_name = 'Around the Horn' 
OR ship_name = 'Ernst Handel';
```
orders: **order_id**, **customer_id**, employee_id, order_date, required_date, shipped_date, ship_via, freight, **ship_name**
order_details: **order_id**, product_id, unit_price, quantity
products: **product_id**, product_name, supplier_id, category_id


3. finner produktnavnet på alle produkter hvor totalverdien på lager er større enn 1000, og hvor produktets pakkemåte måles i kilogram eller gram. (29)
```sql
SELECT product_name 
FROM products 
WHERE (units_in_stock * unit_price) > 1000
AND quantity_per_unit LIKE '% kg %'
OR quantity_per_unit LIKE '% g %';
```

6. finner produktnavnet på det produktet som er solgt for en pris (som oppgitt i order_details) med størst differanse fra nåværende pris (som oppgitt i products).
```sql

```