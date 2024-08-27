# Домашнее задание к занятию 12.04 - "`«SQL. Часть 2»`" - `Чибриков Станислав`

### Задание 1

Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию: 
- фамилия и имя сотрудника из этого магазина;
- город нахождения магазина;
- количество пользователей, закреплённых в этом магазине.

*Ответ:*

```sql
SELECT CONCAT(s.last_name, ' ', s.first_name) AS staff, c.city, COUNT(c2.store_id) AS custumers
FROM customer c2
INNER JOIN store s2 ON s2.store_id = c2.store_id
INNER JOIN staff s ON s.staff_id = s2.manager_staff_id 
INNER JOIN address a ON s.address_id = a.address_id
INNER JOIN city c ON c.city_id = a.city_id
GROUP BY c2.store_id
HAVING COUNT(c2.store_id) > 300;
```
---
### Задание 2

Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.

*Ответ:*

```sql
SELECT COUNT(f.title) 
FROM film f
WHERE f.`length` > (SELECT AVG(`length`) FROM film)
```
---
### Задание 3

Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.

*Ответ:*

```sql
SELECT DATE_FORMAT(payment_date, '%Y-%m') AS payment_month, COUNT(rental_id) AS rental_count, SUM(amount) AS total_amount 
FROM payment 
GROUP BY payment_month 
ORDER BY total_amount DESC 
LIMIT 1;
```
---


