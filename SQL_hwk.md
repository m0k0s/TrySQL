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
  	
* 6d. How many copies of the film `Hunchback Impossible` exist in the inventory system?

* 6e. Using the tables `payment` and `customer` and the `JOIN` command, list the total paid by each customer. List the customers alphabetically by last name:

  ```
  	![Total amount paid](Images/total_payment.png)
  ```

* 7a. The music of Queen and Kris Kristofferson have seen an unlikely resurgence. As an unintended consequence, films starting with the letters `K` and `Q` have also soared in popularity. Use subqueries to display the titles of movies starting with the letters `K` and `Q` whose language is English. 

* 7b. Use subqueries to display all actors who appear in the film `Alone Trip`.
   
* 7c. You want to run an email marketing campaign in Canada, for which you will need the names and email addresses of all Canadian customers. Use joins to retrieve this information.

* 7d. Sales have been lagging among young families, and you wish to target all family movies for a promotion. Identify all movies categorized as famiy films.

* 7e. Display the most frequently rented movies in descending order.
  	
* 7f. Write a query to display how much business, in dollars, each store brought in.

* 7g. Write a query to display for each store its store ID, city, and country.
  	
* 7h. List the top five genres in gross revenue in descending order. (**Hint**: you may need to use the following tables: category, film_category, inventory, payment, and rental.)
  	
* 8a. In your new role as an executive, you would like to have an easy way of viewing the Top five genres by gross revenue. Use the solution from the problem above to create a view. If you haven't solved 7h, you can substitute another query to create a view.
  	
* 8b. How would you display the view that you created in 8a?

* 8c. You find that you no longer need the view `top_five_genres`. Write a query to delete it.

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
