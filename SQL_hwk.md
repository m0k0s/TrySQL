## Homework Assignment

* 1a. Display the first and last names of all actors from the table `actor`. 
SELECT * FROM `actor`
SELECT actor.first_name, actor.last_name FROM actor

* 1b. Display the first and last name of each actor in a single column in upper case letters. Name the column `Actor Name`. 
ALTER TABLE `actor` ADD `actor_name` VARCHAR(50) NOT NULL ;

* 2a. You need to find the ID number, first name, and last name of an actor, of whom you know only the first name, "Joe." What is one query would you use to obtain this information?
SELECT actor.actor_id, actor.first_name, actor.last_name FROM actor WHERE actor.first_name = "Joe"
  	
* 2b. Find all actors whose last name contain the letters `GEN`:
SELECT * FROM actor WHERE actor.last_name LIKE `%gen%`
  	
* 2c. Find all actors whose last names contain the letters `LI`. This time, order the rows by last name and first name, in that order:
SELECT * FROM actor WHERE actor.last_name LIKE `%LI%` ORDER BY actor.last_name, actor.first_name

* 2d. Using `IN`, display the `country_id` and `country` columns of the following countries: Afghanistan, Bangladesh, and China: 
(Is this a trick question? Country_id and Country are not columns in this table.)
SELECT country_id, country FROM actor WHERE Country IN ('Afghanistan', 'Bangladesh', 'China');

* 3a. Add a `middle_name` column to the table `actor`. Position it between `first_name` and `last_name`. Hint: you will need to specify the data type.
ALTER TABLE `actor` ADD `middle_name` CHAR(50) NOT NULL ;
ALTER TABLE `actor` CHANGE `middle_name` `middle_name` CHAR(50) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL AFTER `first_name`
  	
* 3b. You realize that some of these actors have tremendously long last names. Change the data type of the `middle_name` column to `blobs`.
ALTER TABLE `actor` CHANGE `middle_name` `middle_name` BLOB NULL DEFAULT NULL;

* 3c. Now delete the `middle_name` column.
"ALTER TABLE `actor` DROP `middle_name`

* 4a. List the last names of actors, as well as how many actors have that last name.
SELECT actor.last_name, COUNT(*) FROM `actor` GROUP BY actor.last_name HAVING COUNT(*) >1


SELECT actor.last_name, COUNT(*) FROM `actor` GROUP BY actor.last_name HAVING COUNT(*) >1


last_name	COUNT(*)	
AKROYD	3	
ALLEN	3	
BAILEY	2	
BENING	2	
BERRY	3	
BOLGER	2	
BRODY	2	
CAGE	2	
CHASE	2	
CRAWFORD	2	
CRONYN	2	
DAVIS	3	
DEAN	2	
DEE	2	
DEGENERES	3	
DENCH	2	
DEPP	2	
DUKAKIS	2	
FAWCETT	2	
GARLAND	3	
GOODING	2	
GUINESS	3	
HACKMAN	2	
HARRIS	3	
HOFFMAN	3	
HOPKINS	3	
HOPPER	2	
JACKMAN	2	
JOHANSSON	3	
KEITEL	3	
KILMER	5	
MCCONAUGHEY	2	
MCKELLEN	2	
MCQUEEN	2	
MONROE	2	
MOSTEL	2	
NEESON	2	
NOLTE	4	
OLIVIER	2	
PALTROW	2	
PECK	3	
PENN	2	
SILVERSTONE	2	
STREEP	2	
TANDY	2	
TEMPLE	4	
TORN	3	
TRACY	2	
WAHLBERG	2	
WEST	2	
WILLIAMS	3	
WILLIS	3	
WINSLET	2	
WOOD	2	
ZELLWEGER	3	


  	
* 4b. List last names of actors and the number of actors who have that last name, but only for names that are shared by at least two actors

SELECT actor.last_name, COUNT(*) FROM `actor` GROUP BY actor.last_name HAVING COUNT(*) >=2


last_name	COUNT(*)	
AKROYD	3	
ALLEN	3	
BAILEY	2	
BENING	2	
BERRY	3	
BOLGER	2	
BRODY	2	
CAGE	2	
CHASE	2	
CRAWFORD	2	
CRONYN	2	
DAVIS	3	
DEAN	2	
DEE	2	
DEGENERES	3	
DENCH	2	
DEPP	2	
DUKAKIS	2	
FAWCETT	2	
GARLAND	3	
GOODING	2	
GUINESS	3	
HACKMAN	2	
HARRIS	3	
HOFFMAN	3	


  	
* 4c. Oh, no! The actor `HARPO WILLIAMS` was accidentally entered in the `actor` table as `GROUCHO WILLIAMS`, the name of Harpo's second cousin's husband's yoga teacher. Write a query to fix the record.
SELECT actor.first_name, actor.last_name, actor.actor_id FROM `actor` WHERE actor.first_name = 'GROUCHO'; 
UPDATE actor SET actor.first_name = 'HARPO' WHERE actor.actor_id = 172;
SELECT actor.first_name, actor.last_name, actor.actor_id FROM actor WHERE actor.actor_id = 172
  	
* 4d. Perhaps we were too hasty in changing `GROUCHO` to `HARPO`. It turns out that `GROUCHO` was the correct name after all! In a single query, if the first name of the actor is currently `HARPO`, change it to `GROUCHO`. Otherwise, change the first name to `MUCHO GROUCHO`, as that is exactly what the actor will be with the grievous error. BE CAREFUL NOT TO CHANGE THE FIRST NAME OF EVERY ACTOR TO `MUCHO GROUCHO`, HOWEVER! (Hint: update the record using a unique identifier.)
UPDATE actor SET actor.first_name = 'GROUCHO' WHERE actor.actor_id = 172;

* 5a. You cannot locate the schema of the `address` table. Which query would you use to re-create it? 

SELECT * FROM INFORMATION_SCHEMA.COLUMNS WHERE TABLE_NAME='address'

* 6a. Use `JOIN` to display the first and last names, as well as the address, of each staff member. Use the tables `staff` and `address`:
SELECT staff.first_name, staff.last_name, address.address, address.city_id, address.postal_code, address.address_id  
FROM `address`
INNER JOIN staff ON staff.address_id = address.address_id



* 6b. Use `JOIN` to display the total amount rung up by each staff member in August of 2005. Use tables `staff` and `payment`. 
SELECT staff.first_name, staff.last_name, payment.amount, payment.staff_id, payment.payment_date FROM `payment` INNER JOIN staff ON staff.staff_id = payment.staff_id; 
SELECT * FROM `staff` 


  	
* 6c. List each film and the number of actors who are listed for that film. Use tables `film_actor` and `film`. Use inner join.
  SELECT f.title, COUNT(fa.actor_id) AS 'Actors'
  FROM film_actor AS fa
  INNER JOIN film as f
  ON f.film_id = fa.film_id
  GROUP BY f.title
  ORDER BY Actors desc;

* 6d. How many copies of the film `Hunchback Impossible` exist in the inventory system?
  SELECT title, COUNT(inventory_id) AS '# of copies'
  FROM film
  INNER JOIN inventory
  USING (film_id)
  WHERE title = 'Hunchback Impossible'
  GROUP BY title;


* 6e. Using the tables `payment` and `customer` and the `JOIN` command, list the total paid by each customer. List the customers alphabetically by last name:
 SELECT c.first_name, c.last_name, SUM(p.amount) AS 'Total Amount Paid'
  FROM payment AS p 
  JOIN customer AS c
  ON p.customer_id = c.customer_id
  GROUP BY c.customer_id
  ORDER BY c.last_name;



* 7a. The music of Queen and Kris Kristofferson have seen an unlikely resurgence. As an unintended consequence, films starting with the letters `K` and `Q` have also soared in popularity. Use subqueries to display the titles of movies starting with the letters `K` and `Q` whose language is English. 
  SELECT title
  FROM film
  WHERE title LIKE 'K%'
  OR title LIKE 'Q%'
  AND language_id IN
  (
   SELECT language_id
   FROM language
   WHERE name = 'English'
  );


* 7b. Use subqueries to display all actors who appear in the film `Alone Trip`.
  SELECT first_name, last_name
  FROM actor 
  WHERE actor_id IN 
  (
    SELECT actor_id
    FROM film_actor
    WHERE film_id = 
    (
       SELECT film_id
       FROM film
       WHERE title = 'Alone Trip'
      )
   );

   
* 7c. You want to run an email marketing campaign in Canada, for which you will need the names and email addresses of all Canadian customers. Use joins to retrieve this information.
  SELECT first_name, last_name, email, country
  FROM customer cus
  JOIN address a
  ON (cus.address_id = a.address_id)
  JOIN city cit
  ON (a.city_id = cit.city_id)
  JOIN country ctr
  ON (cit.country_id = ctr.country_id)
  WHERE ctr.country = 'CANADA';


* 7d. Sales have been lagging among young families, and you wish to target all family movies for a promotion. Identify all movies categorized as famiy films.
  SELECT title, c.name
  FROM film f
  JOIN film_category fc
  ON (f.film_id = fc.film_id)
  JOIN category c
  ON (c.category_id = fc.category_id)
  WHERE name = 'family';


* 7e. Display the most frequently rented movies in descending order.
  SELECT title, COUNT(title) as 'Rentals'
  FROM film
  JOIN inventory
  ON (film.film_id = inventory.film_id)
  JOIN rental
  ON (inventory.inventory_id = rental.inventory_id)
  GROUP by title
  ORDER BY rentals desc;

  	
* 7f. Write a query to display how much business, in dollars, each store brought in.
  SELECT s.store_id, SUM(amount) AS Gross
  FROM payment p
  JOIN rental r
  ON (p.rental_id = r.rental_id)
  JOIN inventory i
  ON (i.inventory_id = r.inventory_id)
  JOIN store s
  ON (s.store_id = i.store_id)
  GROUP BY s.store_id; 


* 7g. Write a query to display for each store its store ID, city, and country.
  SELECT store_id, city, country
  FROM store s
  JOIN address a
  ON (s.address_id = a.address_id)
  JOIN city cit
  ON (cit.city_id = a.city_id)
  JOIN country ctr
  ON(cit.country_id = ctr.country_id);  

* 7h. List the top five genres in gross revenue in descending order. (**Hint**: you may need to use the following tables: category, film_category, inventory, payment, and rental.)
SELECT SUM(amount) AS 'Total Sales', c.name AS 'Genre'
  FROM payment p
  JOIN rental r
  ON (p.rental_id = r.rental_id)
  JOIN inventory i
  ON (r.inventory_id = i.inventory_id)
  JOIN film_category fc
  ON (i.film_id = fc.film_id)
  JOIN category c
  ON (fc.category_id = c.category_id)
  GROUP BY c.name
  ORDER BY SUM(amount) DESC;

  	
* 8a. In your new role as an executive, you would like to have an easy way of viewing the Top five genres by gross revenue. Use the solution from the problem above to create a view. If you haven't solved 7h, you can substitute another query to create a view.
 CREATE VIEW top_five_genres AS
  SELECT SUM(amount) AS 'Total Sales', c.name AS 'Genre'
  FROM payment p
  JOIN rental r
  ON (p.rental_id = r.rental_id)
  JOIN inventory i
  ON (r.inventory_id = i.inventory_id)
  JOIN film_category fc
  ON (i.film_id = fc.film_id)
  JOIN category c
  ON (fc.category_id = c.category_id)
  GROUP BY c.name
  ORDER BY SUM(amount) DESC
  LIMIT 5;

  	
* 8b. How would you display the view that you created in 8a?
  SELECT * FROM top_five_genres;


* 8c. You find that you no longer need the view `top_five_genres`. Write a query to delete it.
  DROP VIEW top_five_genres;

### Appendix: List of Tables in the Sakila DB

* A schema is also available as `sakila_schema.svg`. Open it with a browser to view.

```sql
	'actor'
	'actor_info'
	'address'
	'category'
	'city'
	'country'
	'customer'
	'customer_list'
	'film'
	'film_actor'
	'film_category'
	'film_list'
	'film_text'
	'inventory'
	'language'
	'nicer_but_slower_film_list'
	'payment'
	'rental'
	'sales_by_film_category'
	'sales_by_store'
	'staff'
	'staff_list'
	'store'
```
