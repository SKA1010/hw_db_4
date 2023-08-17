# Домашнее задание к занятию «SQL. Часть 2»

---

Задание можно выполнить как в любом IDE, так и в командной строке.

### Задание 1

Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию: 
- фамилия и имя сотрудника из этого магазина;
- город нахождения магазина;
- количество пользователей, закреплённых в этом магазине.

### Решение 1

Создал запрос:

```sql
SELECT CONCAT_WS(' ', s2.first_name, s2.last_name) AS staff, c.city, COUNT(c2.customer_id) as customers
FROM sakila.store s 
JOIN sakila.address a ON a.address_id = s.address_id 
JOIN sakila.city c ON c.city_id = a.city_id 
JOIN sakila.staff s2 ON s2.store_id = s.store_id 
JOIN sakila.customer c2 ON c2.store_id = s.store_id 
GROUP BY s.store_id, s2.staff_id 
HAVING COUNT(c2.customer_id) > 300 ;
```
Пример выполнения:

![1](https://github.com/SKA1010/hw_db_4/assets/125235217/97035f9e-7a1b-4d57-b7b6-3c4e0a9d1724)

### Задание 2

Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.

### Решение 2

Создал запрос:

```sql
SELECT COUNT(1) 
FROM sakila.film 
WHERE length > (SELECT AVG(length) FROM sakila.film);
```
Пример выполнения:

![2](https://github.com/SKA1010/hw_db_4/assets/125235217/5720c6ea-6a17-40a7-81eb-7d125141f49f)

### Задание 3

Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.

### Решение 3

Создал запрос:

```sql
SELECT	SUM(amount) AS monthly_payment,	DATE_FORMAT(payment_date,'%Y-%m') AS 'month', COUNT(*) AS rental_qnty
FROM payment 
GROUP BY DATE_FORMAT(payment_date,'%Y-%m')
ORDER BY monthly_payment DESC
LIMIT 1;
```
Пример выполнения:

![image](https://github.com/SKA1010/hw_db_4/assets/125235217/3e0f4ecb-dc26-4dc6-ad42-bf4c3ca79ccb)





