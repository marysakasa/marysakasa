SELECT * FROM actor;

SELECT first_name, last_name FROM actor

SELECT title FROM film ORDER BY title

SELECT * FROM address WHERE postal_code IS NULL ORDER BY address_id

SELECT name FROM language ORDER BY name

SELECT name FROM language

SELECT last_name, first_name, email FROM customer ORDER BY last_name

SELECT DISTINCT rating FROM film ORDER BY rating

SELECT title FROM film ORDER BY length DESC LIMIT 5

SELECT title, description, release_year FROM film ORDER BY title LIMIT 10

SELECT title, description, release_year FROM film ORDER BY title LIMIT 10 OFFSET 20

SELECT title, rental_rate, length FROM film ORDER BY rental_rate DESC, length 

SELECT title, release_year FROM film ORDER BY length DESC, replacement_cost LIMIT 1

SELECT title, description, length FROM film WHERE length>180 ORDER BY length;

SELECT * FROM staff WHERE store_id=1

SELECT customer_id, first_name, last_name FROM customer WHERE active=1

SELECT * FROM actor WHERE first_name='Scarlett'

SELECT title FROM film WHERE description LIKE "%student%" ORDER BY title

SELECT title, release_year, length FROM film WHERE length>180 ORDER BY length

SELECT title, release_year, length from film INNER JOIN film_category ON film.film_id=film_category.film_id INNER JOIN category ON film_category.category_id=category.category_id WHERE category.name='Comedy' AND length>180 ORDER BY length

SELECT last_name, first_name, email FROM customer WHERE last_name NOT LIKE "%A%" AND first_name NOT LIKE "%A%" ORDER BY customer_id

SELECT title, description, release_year FROM film WHERE rating='NC-17' AND description LIKE "%Database Administrator%" ORDER BY title

SELECT title, description, release_year FROM film WHERE rating IN ('PG','PG-13') AND (description LIKE '%Dog%' OR description LIKE '%Cat%') ORDER BY title

SELECT title, rating FROM film WHERE rating IN ('R', "NC-17") ORDER BY title

SELECT title, rating FROM film WHERE rating IN ('PG', 'PG-13') ORDER BY title

SELECT EMPLOYEE.EMP_NO, EMPLOYEE.FIRST_NAME, EMPLOYEE.LAST_NAME, EMPLOYEE.HIRE_DATE, EMPLOYEE.JOB_CODE FROM EMPLOYEE INNER JOIN EMPLOYEE_PROJECT ON EMPLOYEE.EMP_NO=EMPLOYEE_PROJECT.EMP_NO INNER JOIN PROJECT ON EMPLOYEE_PROJECT.PROJ_ID=PROJECT.PROJ_ID WHERE PROJECT.PROJ_NAME='Video Database' ORDER BY EMPLOYEE.LAST_NAME, EMPLOYEE.JOB_CODE

SELECT * FROM employee e WHERE job_country NOT LIKE 'USA'

SELECT full_name, hire_date FROM employee WHERE hire_date LIKE '1992%' ORDER BY hire_date

SELECT title AS film_title FROM film LEFT JOIN inventory ON film.film_id=inventory.film_id WHERE inventory_id IS NULL;

SELECT f.title, c.name FROM film f LEFT JOIN film_category fc ON f.film_id=fc.film_id JOIN category c ON fc.category_id=c.category_id

SELECT email, SUBSTRING_INDEX(email,'@',1) AS address, SUBSTRING_INDEX(email,'@',-1) AS domain FROM customer ORDER BY email

DESC address

SHOW INDEX from film

SELECT f.title, f.release_year FROM film f LEFT JOIN film_actor fa USING (film_id) WHERE fa.actor_id IS NULL ORDER BY f.title

SELECT 
  c1.customer_id, c1.first_name, c1.last_name,
  c2.customer_id, c2.first_name, c2.last_name 
FROM customer c1
JOIN customer c2 ON c1.first_name = c2.last_name
WHERE c1.customer_id != c2.customer_id
ORDER BY c1.customer_id;

SELECT title FROM film f JOIN inventory i USING (film_id)
LEFT JOIN rental r USING (inventory_id)
    WHERE r.rental_id IS NULL 
    ORDER BY f.title

SELECT f.film_id, f.title, c.name AS category FROM film f
JOIN film_category fc USING (film_id)
JOIN category c USING (category_id)
WHERE c.name IN ('Comedy', 'Music', 'Travel')
ORDER BY Film_id

SELECT first_name, last_name FROM customer
WHERE LEFT (first_name,1)=LEFT(last_name,1)
ORDER BY first_name, last_name

SELECT f.title, rating FROM film f 
JOIN inventory USING (film_id)
JOIN rental USING (inventory_id)
JOIN customer c USING (customer_id)
WHERE (c.first_name='KATIE' AND c.last_name='ELLIOTT')
ORDER BY CASE WHEN rating='R' THEN 1 ELSE 2 END, title


SELECT address_id, postal_code FROM address WHERE postal_code % 2 = 0 ORDER BY address_id

WITH combined_data AS (
SELECT 'customer' as record_type, last_name, first_name, email FROM customer
UNION ALL
SELECT 'employee' as record_type, last_name, first_name, email FROM staff )
SELECT * FROM combined_data
ORDER BY last_name, first_name
