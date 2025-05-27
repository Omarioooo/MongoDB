# <span style="color: #1E3A8A;">MongoDB and NoSQL Comprehensive Cheat Sheet</span>

🚀 A complete guide to NoSQL and MongoDB concepts, commands, and best practices.

---

## <span style="color: #0D9488;">🌐 NoSQL Overview</span>

- NoSQL databases are **non-relational**, **distributed systems designed** to handle large-scale, diverse data with **flexible schemas** & excellent in **scalability** and **performance** for modern applications.
  
- SQL databases, which **fixed**, **static**, or **predefined schema** and **tabular structures**.

### <span style="color: #C2410C;">SQL vs. NoSQL</span>

| Key                     | SQL (Relational)                              | NoSQL (Non-Relational)                       |
|-------------------------|-----------------------------------------------|---------------------------------------------|
| **Type**                | Relational Database Management System (_**RDBMS**_) | Non-relational or distributed database (_**Not Only SQL**_)     |
| **Schema**              | Fixed, static, predefined schema              | Dynamic schema                              |
| **Use Case**            | Not suited for hierarchical data storage      | Best for hierarchical data storage          |
| **Scalability**         | Vertically scalable (e.g., increase CPU, RAM) | Horizontally scalable (e.g., add more servers) |
| **Properties**          | Follows ACID (Atomicity, Consistency, Isolation, Durability) | Follows CAP (Consistency, Availability, Partition Tolerance) |
| **Examples**            | MySQL, PostgreSQL, Oracle, MS-SQL Server      | MongoDB, Cassandra, HBase, Neo4j            |

### <span style="color: #C2410C;">CAP Theorem</span>
The **_CAP_** theorem states that a distributed database can **only guarantee two out of three properties**:
- **Consistency**: All nodes see the `same data` at the same time.
- **Availability**: Every request receives a response, even if some nodes are down.
- **Partition Tolerance**: The system continues to operate despite network partitions.

NoSQL databases prioritize **Availability** and **Partition Tolerance** (AP) or **Consistency** and **Partition Tolerance** (CP), depending on the system, unlike SQL databases, which emphasize **ACID** compliance.

### <span style="color: #C2410C;">ACID Properties</span>
SQL databases follow **ACID** properties to ensure reliable transactions:
- **Atomicity**: Ensures all parts of a transaction complete, or none do.
- **Consistency**: Maintains `data integrity` before and after transactions.
- **Isolation**: Transactions are processed independently without interference.
- **Durability**: Committed transactions are permanently saved, even in failures.

NoSQL databases, like MongoDB, may relax ACID properties to prioritize **scalability** and **performance**, though MongoDB supports ACID transactions in certain configurations.

### <span style="color: #C2410C;">Data Types in NoSQL</span>
NoSQL databases handle three types of data:
- **Structured Data**:
  - Tabular data with rows and columns, like in relational databases.
  - All rows in a table have the same columns.
  - Managed using SQL (Structured Query Language).
  - Example: Customer records with fixed fields (ID, Name, Address).
- **Semi-Structured Data**:
  - Data with some structure but not rigid like relational tables.
  - Often stored in JSON, XML, or key-value formats.
  - Includes document databases (e.g., MongoDB), key-value stores, and graph databases.
  - Example: JSON document with varying fields per record.
- **Unstructured Data**:
  - Data without a predefined model, such as text-heavy content, videos, audio, or binary files.
  - May include numbers, dates, or facts but lacks a consistent structure.
  - Example: Social media posts, multimedia files.

### <span style="color: #C2410C;">Why NoSQL? (3V + 1C)</span>
- NoSQL databases are driven by the challenges of **Big Data**, characterized by:
  - **Volume**: Handling terabytes or petabytes of data.
  - **Velocity**: High-speed data ingestion from multiple sources (e.g., IoT, social media).
  - **Variety**: Managing structured, semi-structured, and unstructured data.
  - **Complexity**: Data stored across multiple locations or data centers.

- NoSQL excellent in:
  - High read/write throughput (e.g., social media platforms).
  - Horizontal scalability across multiple nodes (clusters).
  - Handling complex, distributed data environments where SQL performance degrades.

---

## <span style="color: #0D9488;">📄 MongoDB Overview</span>

- **MongoDB** is a **document-oriented NoSQL database**.
- Written in **C++**.
- Uses **sharding** to split large databases into smaller, manageable pieces (shards).
- Stores data as **BSON** (Binary JSON).
- Each document has a **primary key** called `_id` (automatically generated if not specified).

### <span style="color: #C2410C;">Why MongoDB?</span>
MongoDB is a leading NoSQL database due to:
- **MEAN Stack**: Integrates seamlessly with MongoDB, Express.js, Angular, Node.js.
- **Open Source**: Freely available and community-driven.
- **High Write Load**: Prioritizes high insert rates over transaction safety, ideal for low-value, high-volume data (e.g., logs, events).
- **High Availability**: Built-in **replica sets** (master-slave servers) ensure instant, automatic recovery from node or data center failures, even in unreliable environments.
- **Scalability**: Easily scales horizontally for large datasets (beyond 1GB) without performance degradation, unlike RDBMS tables (e.g., MySQL slows at 5-10GB).
- **Flexible Schema**: Adding new fields doesn’t lock the database or degrade performance, unlike RDBMS.
- **Location-Based Queries**: Built-in geospatial functions for fast, accurate location-based data retrieval.
- **No DBA Required**: Simplifies data management without needing complex normalization or joins, ideal for teams without dedicated database administrators.

**Note**: For large-scale deployments, follow MongoDB best practices to avoid pitfalls (see [mongodb.com/use-cases](http://www.mongodb.com/use-cases)).

### <span style="color: #C2410C;">🪪 MongoDB ObjectId</span>
The `_id` field in MongoDB is a 12-byte **ObjectId** with:
- **4-byte timestamp**: Creation time in seconds since the Unix epoch.
- **5-byte random value**: Unique per machine and process.
- **3-byte counter**: Incrementing, initialized randomly.

Example:
```javascript
"_id": ObjectId("507f1f77bcf86cd799439011")
```
> ⚠️ **_ObjectId_** can be given to any field else
> 
> Example:-
>```javascript
>"userId": ObjectId("507afa7bcaf87cd756238230")
>```


> 📌 By default mongodb gives _id to your document
>  ```javascript
>  {
>    "name": "Omar",
>    "age": 13,
>    "address": { "city": "Alexandria", "zip": "12345" }
>  }
> ```
> Mongodb read it as....
>  ```javascript
>  {
>    "_id": ObjectId("507f191e810c19729de860ea"),
>    "name": "Omar",
>    "age": 13,
>    "address": { "city": "Alexandria", "zip": "12345" }
>  }
>```



> 🖇️ **_id** can be any thing else instead of the **ObjectId("__")**
>  ```javascript
>  {
>    "_id": 1,      
>    "name": "Omar",
>    "age": 13,
>    "address": { "city": "Alexandria", "zip": "12345" }
>  }
> ```
 
> 📌 **If** _id **is not specified, MongoDB `assigns` a unique ObjectId.**
> 
> 📌  **Duplicate** _id values will cause a **`duplicate key error`**.

### <span style="color: #C2410C;">📖 Collections</span>
- Groups of **documents**.
- Equivalent to an RDBMS **table**.
- **Schema-less**, allowing flexible document structures.

### <span style="color: #C2410C;">📝 Documents</span>
- Key-value pairs forming a single record.
- **Dynamic schema**, meaning each document can have a different structure.
- Example:
  ```javascript
  {
    "_id": ObjectId("507f191e810c19729de860ea"),
    "name": "Omar",
    "age": 26,
    "address": { "city": "Cairo", "zip": "12345" }
  }
  ```

  ___
  
### <span style="color: #C2410C;">🌐 RDBMS vs MongoDB</span>

| RDBMS           | MongoDB             |
|-----------------|---------------------|
| Database        | Database            |
| Table           | Collection          |
| Row / Tuple     | Document            |
| Column          | Field               |
| Table Join      | Embedded Documents  |
| Primary Key     | `_id` Field         |

---

## <span style="color: #0D9488;">📊 MongoDB Data Types</span>

MongoDB supports a variety of data types for flexible data modeling:

| Data Type               | Description                                        | Example                                               |
|-------------------------|----------------------------------------------------|-------------------------------------------------------|
| **String**              | UTF-8 text                                         | `"name": "Omar"`                                      |
| **Integer (int32, int64)** | Numerical values (`int32`, `int64`)              | `"age": 21`                                           |
| **Double**              | 64-bit floating-point                              | `"price": 19.99`                                      |
| **Decimal128**          | High-precision decimal                             | `"balance": NumberDecimal("1234.56")`                 |
| **Boolean**             | `true` or `false`                                  | `"isActive": true`                                    |
| **Array**               | Multiple values in one field                       | `"hobbies": ["coding", "music"]`                      |
| **Object**              | Embedded document (sub-document)                   | `"address": {"city": "Cairo", "zip": "12345"}`        |
| **ObjectId**            | Unique ID generated by MongoDB                     | `"_id": ObjectId("507f1f77bcf86cd799439011")`        |
| **Date**                | UTC Date & Time                                    | `"createdAt": ISODate("2025-04-14T09:00:00Z")`        |
| **Null**                | `null` value                                       | `"deletedAt": null`                                   |
| **Binary Data (BinData)** | Stores binary files                               | `"fileData": BinData(0, "MZ...")`                     |
| **Regex**               | Regular Expressions                                | `"pattern": /abc/i`                                   |
| **JavaScript**          | JavaScript code                                    | `"func": function() { return true; }`                 |
| **JavaScript with Scope** | JavaScript code with context                     | `Code("return x + y;", { x: 1, y: 2 })`               |
| **Timestamp**           | System internal timestamp                          | `"lastModified": Timestamp(1642558800, 1)`            |
| **MinKey**              | Minimum BSON type                                  | `{ "minKey": MinKey() }`                              |
| **MaxKey**              | Maximum BSON type                                  | `{ "maxKey": MaxKey() }`                              |

### <span style="color: #C2410C;">Example Document with Data Types</span>
```javascript
db.dataTypesExample.insertOne({
  stringExample: "Hello, MongoDB!",
  intExample: 42,
  longExample: NumberLong("9223372036854775807"),
  doubleExample: 3.14159,
  decimalExample: NumberDecimal("1234567890.123456789"),
  booleanExample: true,
  arrayExample: ["MongoDB", "Java", "Data"],
  objectExample: { city: "Cairo", zipCode: "12345" },
  objectIdExample: ObjectId("507f191e810c19729de860ea"),
  dateExample: ISODate("2025-04-14T12:00:00Z"),
  nullExample: null,
  binaryExample: new BinData(0, "SGVsbG8sIE1vbmdvREEh"),
  regexExample: /Mongo/i,
  javascriptExample: function() { return "Hello from JavaScript!"; },
  javascriptWithScopeExample: new Code("return x + y;", { x: 10, y: 20 }),
  timestampExample: Timestamp(1610000000, 1),
  minKeyExample: MinKey(),
  maxKeyExample: MaxKey()
});
```

---

### <span style="color: #0D9488;">MongoDB: `MinKey` and `MaxKey` Explained in Depth</span>

## <span style="color: #C2410C;">Overview</span>

MongoDB includes two special BSON types that help with range queries and indexing: **`MinKey`** and **`MaxKey`**.

| Type    | Description                             | Common Use                          |
|---------|-----------------------------------------|-------------------------------------|
| MinKey  | Lowest possible BSON value              | Lower bound in range or index query |
| MaxKey  | Highest possible BSON value             | Upper bound in range or index query |

>⚠️ These types are **rarely used in normal applications** but can be **very powerful** when used correctly.

---

## <span style="color: #C2410C;">Syntax</span>

```js
new MinKey();
new MaxKey();
```

### In MongoDB Documents

You can even store them as values in documents:

```js
db.examples.insertOne({
  minKeyExample: new MinKey(),
  maxKeyExample: new MaxKey()
});
```

---

## <span style="color: #C2410C;">Example Collection</span>

Suppose we have the following documents in a collection called `products`:

```json
{ "name": "Laptop", "price": 1000 }
{ "name": "Phone", "price": 500 }
{ "name": "Tablet", "price": 750 }
{ "name": "Charger", "price": 100 }
```

---

## <span style="color: #C2410C;">Use Cases</span>

### ✅ 1. Return All Values Less Than MaxKey

```js
db.products.find({ price: { $lt: new MaxKey() } });
```

Returns **all products** because all numbers are less than `MaxKey`.

---

### ✅ 2. Return All Values Greater Than MinKey

```js
db.products.find({ price: { $gt: new MinKey() } });
```

Also returns **all products** because all numbers are greater than `MinKey`.

---

### ❌ 3. Return Values Greater Than MaxKey

```js
db.products.find({ price: { $gt: new MaxKey() } });
```

Returns **nothing**, since `MaxKey` is already the highest possible value.

---

### ✅ 4. Bounded Range Query

Get prices from the **minimum** up to `800`:

```js
db.products.find({ price: { $gte: new MinKey(), $lte: 800 } });
```

Returns: Phone, Tablet, Charger

---


## <span style="color: #0D9488;">📙 Basic Shell Commands</span>

Start and navigate MongoDB using these commands:

| Command               | Purpose                                       |
|-----------------------|-----------------------------------------------|
| `mongosh`             | Start MongoDB Shell                           |
| `show dbs`            | List all databases                            |
| `use <dbname>`        | Switch to database (creates if non-existent)  |
| `db`                  | Show current database name                    |
| `show collections`    | List all collections in current database      |
| `show users`          | List all users in current database            |
| `db.dropDatabase()`   | Delete current database                       |
| `exit`                | Exit the MongoDB Shell                        |

---

## <span style="color: #0D9488;">📝 CRUD Operations</span>

### <span style="color: #C2410C;">Create Operations</span>
Insert documents into a collection:

**General Formula**

  - `db.collection.insertOne(document)`: Inserts a single document.

  - `db.collection.insertMany([document1, document2, ...])`: Inserts multiple documents.

```javascript
// Insert one document
db.users.insertOne({ name: "Omar", age: 26, country: "Egypt" });

// Insert multiple documents
db.users.insertMany([
  { name: "aboOmer", age: 19 },
  { name: "Omar", age: 25 }
]);
```

### <span style="color: #C2410C;">Read Operations</span>
Query documents from a collection:

**General Formula**

- `db.collection.findOne({filter}, {projection})`: Retrieves the first document matching the filter.

- `db.collection.countDocuments({filter})`: Counts documents matching the filter.


```javascript
{
  "_id" : 1
  "name" : "Omar"
  "address" : {"country" : "Egypt", "city": "Alex", "street": "123 Main St", "zip": "12345"}
  "age" : 20
}

// Find all documents
db.users.find();

// Find documents with a filter
db.users.find({ name: "Omar" });

// Find documents with nested field filter

db.users.find({ "address.street": "123 Main St" });

// Find with projection (include specific fields)
db.users.find({ name: "Omar" }, { name: 1, age: 1, _id: 0 });

// Find with projection (exclude specific fields)
db.users.find({}, { age: 0 });

// Find one document
db.users.findOne({ name: "Omar" });

// Count documents
db.users.countDocuments({ name: "Omar" });
```
> ## 🖇️ Notes..

> - The `{filter}` is **optional**.
>
> - { name: 1, age: 1, `_id : 0` } (valid) || { name: 1, age: 1, `_id : 1` } (valid).
>
> - { name: 1, `age: 1`, _id : 0 } **(valid)** || { name: 1, `age: 0`, _id : 0 } **(invalid)**.
> 
> - **Nested fields** are accessed using **dot notation** (e.g., "address.street").
> 
> - **find() returns a `cursor`; use .toArray() or iteration to view results in some drivers**.
> 
> - **findOne() is ideal for retrieving a single document, returning `null` if no match is found**.


### <span style="color: #C2410C;">Update Operations</span>
Modify existing documents:

**General Formula**
- `db.collection.updateOne({filter}, {update}, {options})`: Updates the first document matching the filter.
- `db.collection.updateMany({filter}, {update}, {options})`: Updates all documents matching the filter.
- `db.collection.replaceOne({filter}, replacement, {options})`: Replaces the first matching document entirely.

```javascript
// Update one document
db.users.updateOne({ age: 20 }, { $set: { age: 21 } });

// Update multiple documents
db.users.updateMany({ age: 12 }, { $inc: { age: 3 } });

// Replace one document
db.users.replaceOne({ age: 12 }, { age: 13 });
```

## **Difference Between update and replace**
> ### Update (updateOne, updateMany):
> 
> Modifies specific fields using operators (e.g., $set, $inc).
> 
> Preserves fields not targeted by the update.
> 
> Example: { $set: { age: 21 } } updates only age, leaving other fields intact.

>### Replace (replaceOne):
>
>Replaces the entire document (except _id) with a new document.
>
>Does not use operators; requires a full document.
>
>Example: { name: "Omar", age: 21 } replaces all fields, removing any not included (e.g., country).


### <span style="color: #C2410C;">Delete Operations</span>
Remove documents from a collection:

**General Formula**
- `db.collection.deleteOne({filter})`: Deletes the first document matching the filter.
- `db.collection.deleteMany({filter})`: Deletes all documents matching the filter.


```javascript
// Delete one document
db.users.deleteOne({ age: 20 });

// Delete multiple documents
db.users.deleteMany({ age: 12 });
```
> ⚠️ An empty filter {} in deleteMany will delete all documents in the collection.

---

## <span style="color: #0D9488;">🛠️ Query Operators</span>

### <span style="color: #C2410C;">Query Filter Operators</span>
Filter documents based on conditions:

| Operator | Description            | Example                                     |
|----------|------------------------|---------------------------------------------|
| `$eq`    | Equal to               | `{ name: { $eq: "Omar" } }`                |
| `$ne`    | Not equal              | `{ name: { $ne: "Omar" } }`                |
| `$gt`    | Greater than           | `{ age: { $gt: 20 } }`                     |
| `$gte`   | Greater than or equal  | `{ age: { $gte: 20 } }`                    |
| `$lt`    | Less than              | `{ age: { $lt: 20 } }`                     |
| `$lte`   | Less than or equal     | `{ age: { $lte: 20 } }`                    |
| `$in`    | Value in array         | `{ name: { $in: ["Omar", "aboOmer"] } }`     |
| `$nin`   | Value not in array     | `{ name: { $nin: ["Omar", "Omariooo"] } }`    |
| `$and`   | Logical AND            | `{ $and: [{ age: 20 }, { name: "Omar" }] }` |
| `$or`    | Logical OR             | `{ $or: [{ age: 20 }, { name: "Omar" }] }` |
| `$not`   | Negation               | `{ name: { $not: { $eq: "Omar" } } }`     |
| `$exists`| Field exists           | `{ name: { $exists: true } }`              |
| `$expr`  | Compare fields         | `{ $expr: { $gt: ["$balance", "$debt"] } }`|

#### <span style="color: #6B21A8;">Implicit vs Explicit `$and`</span>
- **Implicit `$and`** (preferred for different fields):
  ```javascript
  db.restaurants.find({
    cuisine: { $ne: "American" },
    "grades.grade": "A",
    borough: { $ne: "Brooklyn" }
  }).sort({ cuisine: -1 });
  ```
- **Explicit `$and`** (required for same field or complex logic):
  ```javascript
  db.restaurants.find({
    $and: [
      { score: { $gt: 70 } },
      { score: { $lt: 90 } }
    ]
  });
  ```
  Equivalent to:
  ```javascript
  db.restaurants.find({ score: { $gt: 70, $lt: 90 } });
  ```

### <span style="color: #C2410C;">Update Operators</span>
Modify documents during updates:

| Operator  | Purpose              | Example                                     |
|-----------|----------------------|---------------------------------------------|
| `$set`    | Update value         | `{ $set: { name: "Omar" } }`                 |
| `$inc`    | Increment value      | `{ $inc: { age: 2 } }`                     |
| `$rename` | Rename field         | `{ $rename: { age: "years" } }`           |
| `$unset`  | Delete field         | `{ $unset: { age: "" } }`                 |
| `$push`   | Add to array         | `{ $push: { friends: "Omarioo" } }`          |
| `$pull`   | Remove from array    | `{ $pull: { friends: "aboOmer" } }`         |

---

## <span style="color: #0D9488;">🔍 Read Modifiers</span>

Enhance query results with modifiers:

```javascript
// Sort results (1: ascending, -1: descending)
db.users.find().sort({ age: -1 });

// Limit number of results
db.users.find().limit(5);

// Skip initial results
db.users.find().skip(2);

// Pretty print results
db.users.find().pretty();
```

---

## <span style="color: #0D9488;">🔎 Regular Expressions (Regex) in MongoDB</span>

MongoDB supports regex for flexible string matching.

### <span style="color: #C2410C;">Basic Regex Syntax</span>
```javascript
// Match names starting with "Wil"
db.restaurants.find(
  { name: /^Wil/ },
  { restaurant_id: 1, name: 1, borough: 1, cuisine: 1 }
);

// Using $regex
db.restaurants.find(
  { name: { $regex: "^Wil" } },
  { restaurant_id: 1, name: 1, borough: 1, cuisine: 1 }
);
```

### <span style="color: #C2410C;">Regex with Options</span>
```javascript
// Case-insensitive search
db.restaurants.find(
  { name: { $regex: "^wil", $options: "i" } },
  { restaurant_id: 1, name: 1 }
);

// Match anywhere in string
db.restaurants.find({ name: /Wil/ });

// Match names ending with "son"
db.restaurants.find({ name: /son$/ });
```

### <span style="color: #C2410C;">Common Regex Patterns</span>
| Pattern           | Description                            |
|-------------------|----------------------------------------|
| `^abc`            | Starts with `abc`                     |
| `abc$`            | Ends with `abc`                       |
| `abc`             | Contains `abc` anywhere               |
| `a.c`             | Any character between `a` and `c`     |
| `a \| b`             | Matches `a` or `b`                    |
| `[A-Z]`           | Any uppercase letter                  |
| `[^A-Z]`          | Anything except uppercase A-Z        |
| `[0-9]{3}`        | Exactly 3 consecutive digits          |
| `.*`              | Zero or more characters of any type  |

### <span style="color: #C2410C;">Regex Optimization Tips</span>
- **Use anchored regex** (`^`) for better performance, as it allows index usage:
  ```javascript
  db.restaurants.find({ name: /^Wil/ });
  ```
- **Avoid unanchored regex** (e.g., `/Wil/` or `/.*Wil.*/`), as it forces a collection scan:
  ```javascript
  db.restaurants.find({ name: /Wil/ }); // Slower
  ```
- Use `$options: "i"` for case-insensitive searches:
  ```javascript
  db.restaurants.find({ name: { $regex: "^wil", $options: "i" } });
  ```
- Keep regex simple and specific to avoid performance issues.

---

## <span style="color: #0D9488;">🛠️ Array Queries with `$elemMatch`</span>

Query arrays to ensure conditions apply to the same array element:

```javascript
// Match documents where a single grade has score between 80 and 100
db.restaurants.findOne({
  grades: { $elemMatch: { score: { $gt: 80, $lt: 100 } } }
});
```

**Comparison with Basic Array Query**:
```javascript
// Matches any grade with score between 80 and 100
db.restaurants.find({ "grades.score": { $gt: 80, $lt: 100 } }).limit(1);
```

| Feature                | `find().limit(1)`         | `findOne()` with `$elemMatch` |
|------------------------|---------------------------|------------------------------|
| **Return Type**        | Cursor with one doc       | Document directly            |
| **Array Matching**     | Any element matches       | Same element matches         |
| **Use Case**           | Simple array queries      | Multiple conditions on same element |

**When to Use**:
- Use `find().limit(1)` for simple queries on single fields.
- Use `$elemMatch` when multiple conditions must apply to the same array element.

---

## <span style="color: #0D9488;">📈 Aggregation Framework</span>

Perform complex data processing with aggregation pipelines:

```javascript
db.orders.aggregate([
  { $match: { status: "delivered" } },
  { $group: { _id: "$customerId", total: { $sum: "$amount" } } }
]);
```

---

## <span style="color: #0D9488;">🚀 Indexes</span>

Improve query performance with indexes:

```javascript
// Create single-field index
db.users.createIndex({ age: 1 });

// Create compound index
db.users.createIndex({ name: 1, age: -1 });

// List indexes
db.users.getIndexes();

// Drop index
db.users.dropIndex("age_1");
```

**Tip**: Indexes are critical for regex queries with `^` and large datasets.

---

## <span style="color: #0D9488;">💡 Best Practices & Tips</span>

- **Schema Design**: Leverage embedded documents for related data to avoid joins.
- **Query Performance**:
  - Use indexes for frequently queried fields (e.g., `name`, `cuisine`).
  - Prefer anchored regex (`^`) for faster searches.
  - Avoid unanchored regex (`/pattern/`) or `.*` at the start to prevent collection scans.
- **CRUD Operations**: Use `findOne` for single-document retrieval and `limit(1)` for cursor-based queries.
- **Regex**: Use `$options: "i"` for case-insensitive searches and keep patterns simple.
- **Aggregation**: Use `$match` early in pipelines to reduce the dataset.
- **Scalability**: Use replica sets and sharding for high availability and growth.
---
