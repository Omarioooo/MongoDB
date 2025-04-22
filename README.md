# <span style="color: #1E3A8A;">MongoDB and NoSQL Comprehensive Cheat Sheet</span>

🚀 A complete guide to NoSQL and MongoDB concepts, commands, and best practices for beginners and advanced users. Master MongoDB and understand NoSQL databases with this structured cheat sheet!

---

## <span style="color: #0D9488;">🌐 NoSQL Overview</span>

NoSQL databases are non-relational, distributed systems designed to handle large-scale, diverse data with flexible schemas. Unlike SQL databases, which rely on rigid, tabular structures, NoSQL databases excel in scalability and performance for modern applications.

### <span style="color: #C2410C;">SQL vs. NoSQL</span>

| Key                     | SQL (Relational)                              | NoSQL (Non-Relational)                       |
|-------------------------|-----------------------------------------------|---------------------------------------------|
| **Type**                | Relational Database Management System (RDBMS) | Non-relational or distributed database      |
| **Schema**              | Fixed, static, predefined schema              | Dynamic schema                              |
| **Use Case**            | Not suited for hierarchical data storage      | Best for hierarchical data storage          |
| **Scalability**         | Vertically scalable (e.g., increase CPU, RAM) | Horizontally scalable (e.g., add more servers) |
| **Properties**          | Follows ACID (Atomicity, Consistency, Isolation, Durability) | Follows CAP (Consistency, Availability, Partition Tolerance) |
| **Examples**            | MySQL, PostgreSQL, Oracle, MS-SQL Server      | MongoDB, Cassandra, HBase, Neo4j            |

### <span style="color: #C2410C;">CAP Theorem</span>
The CAP theorem states that a distributed database can only guarantee two out of three properties:
- **Consistency**: All nodes see the same data at the same time.
- **Availability**: Every request receives a response, even if some nodes are down.
- **Partition Tolerance**: The system continues to operate despite network partitions.

NoSQL databases prioritize **Availability** and **Partition Tolerance** (AP) or **Consistency** and **Partition Tolerance** (CP), depending on the system, unlike SQL databases, which emphasize **ACID** compliance.

### <span style="color: #C2410C;">ACID Properties</span>
SQL databases follow **ACID** properties to ensure reliable transactions:
- **Atomicity**: Ensures all parts of a transaction complete, or none do.
- **Consistency**: Maintains data integrity before and after transactions.
- **Isolation**: Transactions are processed independently without interference.
- **Durability**: Committed transactions are permanently saved, even in failures.

NoSQL databases, like MongoDB, may relax ACID properties (e.g., eventual consistency) to prioritize scalability and performance, though MongoDB supports ACID transactions in certain configurations.

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
NoSQL databases are driven by the challenges of **Big Data**, characterized by:
- **Volume**: Handling terabytes or petabytes of data.
- **Velocity**: High-speed data ingestion from multiple sources (e.g., IoT, social media).
- **Variety**: Managing structured, semi-structured, and unstructured data.
- **Complexity**: Data stored across multiple locations or data centers.

NoSQL excels in:
- High read/write throughput (e.g., social media platforms).
- Horizontal scalability across multiple nodes (clusters).
- Handling complex, distributed data environments where SQL performance degrades.

---

## <span style="color: #0D9488;">📄 MongoDB Overview</span>

- **MongoDBස

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

### <span style="color: #C2410C;">MongoDB ObjectId</span>
The `_id` field in MongoDB is a 12-byte **ObjectId** with:
- **4-byte timestamp**: Creation time in seconds since the Unix epoch.
- **5-byte random value**: Unique per machine and process.
- **3-byte counter**: Incrementing, initialized randomly.

Example:
```javascript
"_id": ObjectId("507f1f77bcf86cd799439011")
```

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
    "name": "Kyle",
    "age": 26,
    "address": { "city": "Cairo", "zip": "12345" }
  }
  ```

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

```javascript
// Insert one document
db.users.insertOne({ name: "Kyle", age: 26, country: "Egypt" });

// Insert multiple documents
db.users.insertMany([
  { name: "Sara", age: 19 },
  { name: "Omar", age: 25 }
]);
```

### <span style="color: #C2410C;">Read Operations</span>
Query documents from a collection:

```javascript
// Find all documents
db.users.find();

// Find documents with a filter
db.users.find({ name: "Kyle" });

// Find documents with nested field filter
db.users.find({ "address.street": "123 Main St" });

// Find with projection (include specific fields)
db.users.find({ name: "Kyle" }, { name: 1, age: 1, _id: 0 });

// Find with projection (exclude specific fields)
db.users.find({}, { age: 0 });

// Find one document
db.users.findOne({ name: "Kyle" });

// Count documents
db.users.countDocuments({ name: "Kyle" });
```

### <span style="color: #C2410C;">Update Operations</span>
Modify existing documents:

```javascript
// Update one document
db.users.updateOne({ age: 20 }, { $set: { age: 21 } });

// Update multiple documents
db.users.updateMany({ age: 12 }, { $inc: { age: 3 } });

// Replace one document
db.users.replaceOne({ age: 12 }, { age: 13 });
```

### <span style="color: #C2410C;">Delete Operations</span>
Remove documents from a collection:

```javascript
// Delete one document
db.users.deleteOne({ age: 20 });

// Delete multiple documents
db.users.deleteMany({ age: 12 });
```

---

## <span style="color: #0D9488;">🛠️ Query Operators</span>

### <span style="color: #C2410C;">Query Filter Operators</span>
Filter documents based on conditions:

| Operator | Description            | Example                                     |
|----------|------------------------|---------------------------------------------|
| `$eq`    | Equal to               | `{ name: { $eq: "Kyle" } }`                |
| `$ne`    | Not equal              | `{ name: { $ne: "Kyle" } }`                |
| `$gt`    | Greater than           | `{ age: { $gt: 20 } }`                     |
| `$gte`   | Greater than or equal  | `{ age: { $gte: 20 } }`                    |
| `$lt`    | Less than              | `{ age: { $lt: 20 } }`                     |
| `$lte`   | Less than or equal     | `{ age: { $lte: 20 } }`                    |
| `$in`    | Value in array         | `{ name: { $in: ["Kyle", "Mike"] } }`     |
| `$nin`   | Value not in array     | `{ name: { $nin: ["Kyle", "Mike"] } }`    |
| `$and`   | Logical AND            | `{ $and: [{ age: 20 }, { name: "Kyle" }] }` |
| `$or`    | Logical OR             | `{ $or: [{ age: 20 }, { name: "Kyle" }] }` |
| `$not`   | Negation               | `{ name: { $not: { $eq: "Kyle" } } }`     |
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
| `$set`    | Update value         | `{ $set: { name: "Hi" } }`                 |
| `$inc`    | Increment value      | `{ $inc: { age: 2 } }`                     |
| `$rename` | Rename field         | `{ $rename: { age: "years" } }`           |
| `$unset`  | Delete field         | `{ $unset: { age: "" } }`                 |
| `$push`   | Add to array         | `{ $push: { friends: "John" } }`          |
| `$pull`   | Remove from array    | `{ $pull: { friends: "Mike" } }`         |

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
| `a|b`             | Matches `a` or `b`                    |
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
- **Practice**: Experiment with queries in `mongosh` to master MongoDB.

---

## <span style="color: #0D9488;">🌟 Summary</span>

- **NoSQL** databases offer flexibility, scalability, and performance for Big Data, handling structured, semi-structured, and unstructured data.
- **MongoDB** is a powerful NoSQL database with dynamic schemas, high write loads, and built-in features like replica sets and geospatial queries.
- Master **collections**, **documents**, and **BSON** data types for effective data modeling.
- Use **CRUD operations** (`insert`, `find`, `update`, `delete`) for data manipulation.
- Leverage **query operators** (`$eq`, `$ne`, `$gt`, `$and`, `$or`) and **regex** for powerful filtering.
- Optimize queries with **indexes** and anchored regex for performance.
- Practice with `mongosh` and explore the **aggregation framework** for advanced data processing.

**Happy Querying! 🚀**

*By: Omar Mohamed*
