# Домашнее задание к занятию "SQL. Часть 1" - `Мильдзихов Сергей`


---

### Задание 1

Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию:

фамилия и имя сотрудника из этого магазина;
город нахождения магазина;
количество пользователей, закреплённых в этом магазине.


### Ответ

> SELECT s.fam, s.nam, m.city, COUNT(*) AS count_users
> FROM users u
> JOIN shops m ON u.id_shops = m.id
> JOIN sotr s ON m.id_sotr = s.id
> GROUP BY m.id
> HAVING COUNT(*) > 300;


### Задание 2

Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.


### Ответ

> SELECT COUNT(film_id) AS 'number of films'
> FROM (SELECT *, AVG(LENGTH) OVER () AS TIME FROM film) t
> WHERE TIME < LENGTH;


### Задание 3

Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.


### Ответ

> SELECT MONTH(p.payment_date) AS month, SUM(p.amount) AS 'total amount', count(p.rental_id) AS 'rentals by month'
> FROM payment p
> GROUP BY MONTH(p.payment_date)
> ORDER BY SUM(p.amount) DESC
> LIMIT 1;
