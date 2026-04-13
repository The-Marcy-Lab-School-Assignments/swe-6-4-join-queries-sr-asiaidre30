# Short Response: JOIN Queries and Connecting to Postgres

Answer each question below. Write in complete sentences (3–5 per answer).

done in google docs

---

## Question 1

What is the difference between `INNER JOIN` and `LEFT JOIN`? Give a concrete example of when you would use each.

**Your answer:**

The difference between `INNER JOIN` and `LEFT JOIN` is that an `INNER JOIN` only returns rows where there is a match in both tables, while a `LEFT JOIN` returns all rows from the left table even if there is no match in the right table. For example, if I only want users who have bookmarks, I would use an `INNER JOIN` because it filters out users without any matches.

But if I want to see all users, including those with zero bookmarks, I would use a `LEFT JOIN`. That way, I don’t lose any data from the main table.

---

## Question 2

Look at this query. What will it return, and why do users with zero bookmarks still appear in the results?

```sql
SELECT users.username, COUNT(bookmarks.bookmark_id) AS total_bookmarks
FROM users
LEFT JOIN bookmarks ON users.user_id = bookmarks.user_id
GROUP BY users.user_id;
```

**Your answer:**

This query returns each user’s username along with the total number of bookmarks they have. It uses a `LEFT JOIN`, so even if a user has no bookmarks, they will still appear in the results. The `COUNT(bookmarks.bookmark_id)` will just return 0 for those users because there are no matching rows in the bookmarks table. The reason they still appear is that `LEFT JOIN` keeps all rows from the users table, regardless of the conditions.

---

## Question 3

What is the `pg` library and why can't you write SQL directly in a `.js` file without it? And what is a connection pool?

**Your answer:**

So the pg library is what lets a Node.js app talk to a PostgreSQL database. You can’t just write SQL inside a JavaScript file and expect it to run, because JavaScript doesn’t actually understand SQL you need something like pg to send those queries to the database and get results back.

A connection pool is basically a set of reusable database connections. Instead of opening and closing a new connection every single time you run a query, your app just reuses existing ones. That makes things a lot faster and more efficient, especially when you have multiple queries happening at the same time.

---

## Question 4

What is a parameterized query and what problem does it solve? Rewrite the unsafe query below as a safe parameterized query using `pg`:

```js
// Unsafe — never do this!
pool.query(`SELECT * FROM users WHERE username = '${username}'`);
```

**Your answer:**

A parameterized query is a way of safely passing values into a SQL query without directly inserting them into the string.

It helps prevent SQL injection, where someone could mess with your database by entering malicious input. Instead of string interpolation, you use placeholders and pass the values separately.

---
