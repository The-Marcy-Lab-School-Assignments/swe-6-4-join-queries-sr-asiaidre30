# Short Response: JOIN Queries and Connecting to Postgres

Answer each question below. Write in complete sentences (3–5 per answer).

---

## Question 1

What is the difference between `INNER JOIN` and `LEFT JOIN`? Give a concrete example of when you would use each.

**Your answer:**

The difference between `INNER JOIN` and `LEFT JOIN` is that an `INNER JOIN` only returns rows where there is a match in both tables, while a `LEFT JOIN` returns all rows from the left table even if there is no match in the right table. For example, if I only want users who have bookmarks, I would use an `INNER JOIN` because it only returns users with matching bookmarks. If I want to see all users, including users with zero bookmarks, I would use a `LEFT JOIN`. This allows me to keep all of the users from the main table.

---

## Question 2

Look at this query. What will it return, and why do users with zero bookmarks still appear in the results?

```sql
SELECT users.username, COUNT(bookmarks.bookmark_id) AS total_bookmarks
FROM users
LEFT JOIN bookmarks ON users.user_id = bookmarks.user_id
GROUP BY users.user_id;

Question 3
What is the pg library and why can't you write SQL directly in a .js file without it? And what is a connection pool?
Your answer:
The pg library allows a Node.js application to communicate with a PostgreSQL database. JavaScript cannot execute SQL against PostgreSQL by itself, so pg is needed to send SQL queries to the database and receive the results. A connection pool is a collection of reusable database connections that the application can use when it needs to run queries. Using a pool is more efficient than creating a new database connection for every query.


Question 4
What is a parameterized query and what problem does it solve? Rewrite the unsafe query below as a safe parameterized query using pg:
// Unsafe — never do this!
pool.query(`SELECT * FROM users WHERE username = '${username}'`);
Your answer:
A parameterized query safely passes values to SQL without directly inserting them into the query string. It helps prevent SQL injection, which can happen when malicious input is inserted into an SQL statement. With pg, I can use $1 as a placeholder and pass the username separately.
pool.query(
 "SELECT * FROM users WHERE username = $1",
 [username]
);

After you paste it into `short-response.md`, save it and run:

```bash
git status
Then send me what git status says and I'll walk you through the commit/push.
