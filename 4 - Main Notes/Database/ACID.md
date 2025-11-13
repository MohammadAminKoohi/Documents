 
 2024-10-16 18:56

Tags: #Database  #Backend 

# ACID

ACID is a set of properties that ensure that database transactions are processed reliably. These properties stand for **Atomicity**, **Consistency**, **Isolation**, and **Durability**. Together, they guarantee that a transaction is processed in a safe, consistent, and recoverable manner, even in the face of system failures or concurrent operations.

## Atomicity

Atomicity ensures that every transaction is treated as a single, indivisible unit of work. The **all-or-nothing** principle applies: either all of the transaction's operations succeed, or none of them do. If any operation within the transaction fails, the database rolls back to its previous state, ensuring that partial changes never occur.

#### Key Points:
- **Rollback:** In case of failure, all changes made by the transaction are undone.
- **Commit:** Only when all steps in the transaction are successful, the transaction is committed, making changes permanent.
- **Logging:** Transaction management systems typically use logging techniques, such as undo logs, to track changes and revert them if necessary.

#### Example:
Imagine a transaction that involves transferring money from one account to another:
1. Withdraw money from Account A.
2. Deposit money into Account B.

If the withdrawal succeeds but the deposit fails, the transaction is rolled back, and both accounts remain unchanged, maintaining data integrity.

## Consistency

Consistency ensures that a transaction leaves the database in a valid state, respecting all rules, constraints, and triggers defined by the database schema. After a transaction, the database must still adhere to all its integrity rules.

#### Key Points:
- **Validation:** All data written during the transaction must be valid according to constraints such as foreign keys, data types, unique constraints, and other business logic.
- **Integrity checks:** Consistency rules include enforcing database constraints like `NOT NULL`, `UNIQUE`, and foreign key constraints.
- **Error handling:** If any part of the transaction violates these rules, the transaction is aborted, and changes are rolled back.

#### Example:
Suppose there’s a rule that an account balance cannot be negative. If a transaction causes an account to go below zero, the database would reject the transaction, ensuring that invalid data cannot be entered.

## Isolation

Isolation determines how transaction operations are isolated from one another when multiple transactions occur concurrently. Isolation ensures that the intermediate state of a transaction is not visible to other transactions, preventing conflicts between transactions.

#### Isolation Levels:
There are four primary isolation levels, each offering different degrees of protection against anomalies like **dirty reads**, **non-repeatable reads**, and **phantom reads**:

1. **Read Uncommitted:** Allows transactions to see uncommitted changes made by others (prone to dirty reads).
2. **Read Committed:** Ensures a transaction can only see data committed before the transaction started. This prevents dirty reads but allows **non-repeatable reads**.
3. **Repeatable Read:** Guarantees that if a transaction reads a value, it will see the same value throughout the transaction, preventing non-repeatable reads but allowing phantom reads.
4. **Serializable:** The strictest level, ensuring complete isolation. Transactions are executed as if they were running serially, preventing all anomalies but potentially reducing concurrency.

#### Key Points:
- **Concurrency:** Isolation allows multiple users to execute transactions concurrently while ensuring that the outcome is as if the transactions were executed serially.
- **Anomalies:** Lower isolation levels may allow certain anomalies (dirty reads, non-repeatable reads, phantom reads), but they also offer better performance.

#### Example:
If two users are trying to book the last seat on a flight at the same time, isolation ensures that one of the transactions completes first and the second transaction will only see the final, committed state of the seat availability.

## Durability

Durability ensures that once a transaction is committed, the changes it made to the database are **permanent**. Even in the case of a system crash, power failure, or other catastrophic events, the committed data remains intact.

#### Key Points:
- **Persistence:** Once committed, the changes are stored in durable storage (e.g., disk) and will survive a system crash.
- **Write-Ahead Logging (WAL):** Databases often implement durability using techniques like write-ahead logging, which ensures that changes are recorded in a log before the actual data is written.
- **Recovery:** In case of a crash, the database uses the logs to recover the committed transactions and restore the database to its last consistent state.

#### Example:
If a transfer between two accounts is successfully committed and the system crashes right after, the transfer will still be reflected in the accounts when the system is restored, ensuring data durability.

---

## Additional Information

### Transaction Lifecycle

A transaction typically follows this sequence:
1. **Begin Transaction**: Starts a new transaction.
2. **Perform Operations**: SQL operations like `INSERT`, `UPDATE`, `DELETE` are performed within the transaction.
3. **Commit**: The transaction is committed, making all changes permanent.
4. **Rollback**: If an error occurs, the transaction is rolled back, reverting the database to its previous state.

### Error Handling in Transactions

In real-world systems, transactions might encounter issues like:
- **Deadlocks**: Two transactions waiting for each other to release locks, causing them to be stuck. Databases typically handle deadlocks by aborting one transaction.
- **Locking**: Transactions acquire locks on data they modify. Depending on the isolation level, different types of locks (shared or exclusive) may be used to ensure consistency and isolation.

### ACID vs. BASE

In distributed systems, especially with NoSQL databases, the focus may shift from ACID properties to the BASE (Basically Available, Soft state, Eventual consistency) model. BASE systems sacrifice some consistency to achieve higher availability and partition tolerance, making them more suitable for large-scale, distributed applications.

---

## Conclusion

The ACID properties ensure that transactions in a database system are processed reliably and consistently, even in the presence of errors or concurrent access. Atomicity guarantees that all parts of a transaction succeed or fail together, consistency ensures that the database remains in a valid state, isolation protects transactions from interfering with each other, and durability ensures that once committed, data is safe from failure. Together, these properties form the backbone of reliable and trustworthy database systems.

---
