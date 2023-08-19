# SYSTEM DESIGN

## WHAT IS TRANSACTION ?

- A transaction, in the context of database management, is a logical unit of work that consists of one or more database operations.
- These operations can include reading, writing, or modifying data in a database.
- Transactions are used to ensure the integrity, consistency, and reliability of the data stored in a database, even in the presence of failures or concurrent access by multiple users.

### ACID properties

- ### Atomicity:

  - This property ensures that a transaction is treated as a single, indivisible unit of work.
  - It means that either all the operations within the transaction are successfully completed, or none of them are.
  - If any part of the transaction fails, the entire transaction is rolled back, and the database returns to its previous state.

- ### Consistency:

  - This property ensures that the database remains in a consistent state before and after the transaction is executed.
  - In other words, transactions should bring the database from one consistent state to another.
  - In other words, a transaction should not violate any integrity constraints defined on the database, ensuring that the data remains valid.
  - Transactions should bring the database from one consistent state to another. In other words, a transaction should not violate any integrity constraints defined on the database, ensuring that the data remains valid.

- ### Isolation:

  - Transactions should be isolated from each other, meaning that the operations of one transaction should not interfere with the operations of other concurrent transactions.

- ### Durability:

  - Once a transaction is successfully completed, its changes are durable and should be permanently saved in the database, even in the face of system failures.

#### Note:

    Transactions play a crucial role in maintaining data integrity and ensuring that the database remains reliable in multi-user environments. They help prevent issues such as data corruption, inconsistent states, and conflicts that can arise when multiple users are accessing and modifying data simultaneously.

    It's important to note that while transactions provide a powerful mechanism for data management, they also come with some overhead due to locking and coordination mechanisms to maintain isolation and consistency. Therefore, proper consideration should be given to transaction design, isolation levels, and performance trade-offs when designing systems that involve heavy transactional workloads.

## WHAT IS A DATABASE ISOLATION LEVEL ?

- Database isolation levels are an essential concept in database management systems (DBMS) that deal with how transactions interact with each other.
- They define the degree to which the operations within a transaction are isolated from the operations of other concurrent transactions
- In simpler terms, isolation levels determine how much one transaction can "see" the changes made by other transactions that are running concurrently.
- The isolation level of a transaction is set at the beginning of the transaction and remains in effect until the transaction completes.
- The isolation level can be set at the database level, the session level, or the transaction level.

### Isolation levels in SQL

- ### Read Uncommitted

  - This is the lowest isolation level, in which transactions are not isolated from each other.
  - Transactions running at this level may read data that has been modified by other concurrent transactions but not yet committed.
  - This can result in non-repeatable reads, in which a transaction reads the same record twice but sees different data each time.
  - It can also result in phantom reads, in which a transaction re-runs a query returning a set of rows that satisfy a search condition and finds that the set of rows has changed due to another concurrent transaction.
  - The READ UNCOMMITTED isolation level is not supported by all DBMSs.

- ### Read Committed

  - This isolation level guarantees that any data read by a transaction is committed at the moment it reads the data.
  - It also guarantees that any data written by a transaction is not read by any other concurrent transaction until the data is committed.
  - This prevents non-repeatable reads but still allows phantom reads.
  - The READ COMMITTED isolation level is supported by all major DBMSs.

- ### Repeatable Read

  - This isolation level guarantees that any data read by a transaction cannot be modified by other concurrent transactions until the transaction completes.
  - This isolation level guarantees that if a transaction reads the same data twice, it will get the same result both times.
  - This prevents non-repeatable reads and phantom reads but still allows phantom reads.
  - The REPEATABLE READ isolation level is supported by all major DBMSs.

- ### Serializable

  - This is the highest isolation level.
  - It ensures that transactions are executed in a way that their effects are equivalent to running them one after another, i.e., serially.
  - It prevents dirty reads, non-repeatable reads, and phantom reads.
  - but it can also lead to performance issues due to increased locking and reduced concurrency.

          The following table shows the phenomena that can occur under each isolation level.

          | Phenomena                 | Read uncommitted | Read committed | Repeatable read | Serializable |
          | ------------------------- | ---------------- | -------------- | --------------- | ------------ |
          | Dirty read                | Possible         | Not possible   | Not possible    | Not possible |
          | Non-repeatable read       | Possible         | Possible       | Not possible    | Not possible |
          | Phantom read              | Possible         | Possible       | Possible        | Not possible |
          | Lost update               | Possible         | Possible       | Possible        | Not possible |
          | Unrepeatable read         | Possible         | Possible       | Possible        | Not possible |
          | Incorrect summary         | Possible         | Possible       | Possible        | Possible     |
          | Inconsistent analysis     | Possible         | Possible       | Possible        | Possible     |
          | Non-repeatable range read | Possible         | Possible       | Possible        | Possible     |
          | Phantom range read        | Possible         | Possible       | Possible        | Possible     |

## WHAT IS A LOCK IN DATABASES ?

- A lock is a mechanism that prevents multiple users from accessing the same data concurrently.
- Locks are essential for concurrency control, which is a mechanism that prevents conflicts and data anomalies that can arise when multiple users access and modify the same data concurrently.
- Locks are used to protect shared resources in a multi-user environment where multiple transactions can access and modify the same data concurrently.
- Locks can be applied at different levels of granularity. They can be applied to the entire database, a table, a row, or even a single field within a row.

### Types of locks

- There are two main types of locks: shared locks and exclusive locks.
  - A shared lock allows the holder of the lock to read a resource but not modify it. Multiple shared locks can be held on the same resource at the same time.
  - An exclusive lock allows the holder of the lock to both read and modify a resource. Only one exclusive lock can be held on a resource at a time.

### Lock escalation

- Lock escalation is the process of converting a large number

<br>
<br>

## WHAT IS A DATABASE INDEX ?

- A database index is a data structure that improves the speed of data retrieval operations on a database table at the cost of additional writes and storage space to maintain the index data structure.
- Indexes can be created using one or more columns of a database table, providing the basis for both rapid random lookups and efficient access of ordered records.
- An index is a data structure that contains pointers to data in a table or a set of tables in a database.
- Indexes are used to improve the performance of data retrieval operations on a database table.
- Indexes can be created using one or more columns of a database table, providing the basis for both rapid random lookups and efficient access of ordered records.
- Indexes are used to improve the performance of data retrieval operations on a database table.
- Indexes can be created using one or more columns of a database table, providing the basis for both rapid random lookups and efficient access of ordered records.

### Types of indexes

- There are many types of indexes, each with its own advantages and disadvantages. Some of the most common types of indexes are:

  - #### B-tree index

    - A B-tree index is a balanced tree structure that is used to store keys in sorted order, allowing for efficient insertion, deletion, and retrieval of records based on their keys.
    - B-tree indexes are widely used in database systems due to their ability to handle large amounts of data and provide fast lookups.

  - #### Hash index

    - A hash index is a data structure that uses a hash function to map keys to values.
    - Hash indexes are not as flexible as B-tree indexes, but they are very efficient for equality lookups.
    - Hash indexes are not as flexible as B-tree indexes, but they are very efficient for equality lookups.

  - #### Bitmap index

    - A bitmap index is a data structure that uses bitmaps to store the values of a column in a table.
    - Bitmap indexes are very efficient for low-cardinality columns, i.e., columns that contain a small number of distinct values.
    - Bitmap indexes are very efficient for low-cardinality columns, i.e., columns that contain a small number of distinct values.

  - #### R-tree index

    - A R-tree index is a balanced tree structure that is used to store spatial data in a database.
    - R-tree indexes are commonly used in geostatics databases.
    - R-tree indexes are commonly used

### Disadvantages of indexes

Indexes can improve the performance of data retrieval operations, but they also come with some disadvantages:

- Indexes require additional storage space.
- Indexes slow down data insertion, modification, and deletion operations because the indexes also need to be updated.
- Indexes can increase the complexity of the database design.

<br>
<br>

## HOW TO STORE PASSWORDS SAFELY IN THE DATABASE ?

### Things not to do:

- Do not store passwords in plain text.
- Do not store passwords encrypted with symmetric encryption. Symmetric encryption uses a single key to encrypt and decrypt data. The key is shared between the sender and the receiver of the data. If the key is compromised, the data can be decrypted.

### What is salt

- A salt is a random sequence of data that is used to modify a password before it is hashed.
- Salting is a technique that is used to strengthen the security of password hashing.
- It makes it more difficult for attackers to crack passwords using brute force or dictionary attacks.

Example:

```javascript
const crypto = require("crypto");

const password = "password123";

// Generate a random salt
const salt = crypto.randomBytes(16).toString("hex");

// Generate a hash using the password and the salt
const hash = crypto
  .pbkdf2Sync(password, salt, 1000, 64, "sha512")
  .toString("hex");

console.log(`Salt: ${salt}`);
console.log(`Hash: ${hash}`);
```

### How to validate a password

- A client sends a password to the server.
- The system fetches the corresponding salt from the database.
- The system appends the salt to the password and hashes it. Let’s
  call the hashed value H1.
- The system compares H1 with the hashed password stored in the database. If they match, the password is valid; otherwise, the password is invalid.
