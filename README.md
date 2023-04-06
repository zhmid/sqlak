<h1>Sqlak</h1>

  <p>SQLAK is a lightweight PHP class that simplifies writing SQL queries and interacting with databases using the MySQLi extension. This README provides an overview of how to use each of SQLAK's functions.</p>

  <h2>Creating a new database connection</h2>

  <p>To create a new database connection, you need to create a new instance of the <code>sqlak</code> class by passing in the database configuration settings and the name of your database:</p>

  <pre><code>$db = new sqlak(
    'host' =&gt; 'localhost',
    'user' =&gt; 'root',
    'pass' =&gt; 'password'
), 'my_database');</code></pre>

  <p>If you're running MySQL on the default port (3306), you can omit the <code>port</code> key from the configuration array.</p>

  <h2>Executing SQL queries</h2>

  <p>You can execute any type of SQL query using the <code>do()</code> function:</p>

  <pre><code>$db-&gt;do('CREATE TABLE users (id INT AUTO_INCREMENT PRIMARY KEY, name VARCHAR(255), email VARCHAR(255))');</code></pre>

  <p>The <code>do()</code> function returns either a <code>mysqli_result</code> object or <code>false</code> if an error occurred.</p>

  <h2>Selecting rows from a table</h2>

  <p>To select rows from a table, use the <code>sel()</code> function:</p>

  <pre><code>$results = $db-&gt;sel('users', '*', 'age &gt; 30');</code></pre>

  <p>This will return a <code>mysqli_result</code> object that you can loop through to fetch each row:</p>

  <pre><code>while ($row = mysqli_fetch_assoc($results)) {
    echo "{$row['name']} ({$row['age']})\n";
}</code></pre>

  <h2>Inserting rows into a table</h2>

  <p>To insert a new row into a table, use the <code>put()</code> function:</p>

  <pre><code>$db-&gt;put('users', (
    'col' =&gt; ('name', 'age'),
    'val' =&gt; ('John Doe', 32)
));</code></pre>

  <p>This will insert a new row into the <code>users</code> table with a name of "John Doe" and an age of 32.</p>

  <h2>Updating rows in a table</h2>

  <p>To update one or more rows in a table, use the <code>set()</code> function:</p>

  <pre><code>$db-&gt;set('users', (
    'col' =&gt; ('name', 'age'),
    'val' =&gt; ('Jane Doe', 33)
), 'id = 1');</code></pre>

  <p>This will update the row in the <code>users</code> table with an ID of 1 to have a name of "Jane Doe" and an age of 33.</p>

  <h2>Deleting rows from a table</h2>

  <p>To delete one or more rows from a table, use the <code>del()</code> function:</p>

  <pre><code>$db-&gt;del('users', 'age &lt; 18');</code></pre>

  <p>This will delete all rows from the <code>users</code> table where the age is less than 18.</p>

  <h2>Counting rows in a table</h2>

  <p>To count the number of rows in a table that match a certain condition, use the <code>count()</code> function:</p>

  <pre><code>$count = $db-&gt;count('users', 'age &gt; 30');</code></pre>

  <p>This will return the number of rows in the <code>users</code> table where the age is greater than 30.</p>

  <h2>Getting rows as an array</h2>

  <p>If you want to retrieve the results of a SELECT query as an array rather than a <code>mysqli_result</code>
object, use the <code>give()</code> function:</p>

<pre><code>$results = $db->give('users', 'age > 30', 'name, age');</code></pre>

<p>This will return an array of associative arrays representing each row that matches the condition.</p>

<h2>Conclusion</h2>

<p>That's it! With these functions, you can easily execute SQL queries and interact with your MySQL database using PHP. If you have any questions or issues, please don't hesitate to open an issue on GitHub or contribute to the project.</p>
