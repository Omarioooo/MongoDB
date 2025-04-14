# MongoDB
Step by step learning mongodb

## __MongoDB Overview__
___
- **Monog is `Documented Database`.**
- **MongoDB is written in `C++`.**
- **`Sharding` is a database that separates large database into smaller, faster, and easily managed parts. These smaller parts are called data shards. Shard is defined as a "small part of a whole".**
- **MongoDB implements the **__primary key__** using the `_id` field. Every primary key acts as a different identifier for the document. This field is automatically created by MongoDB when the document is inserted. This can be any type, as long as it is different from the collection.**
- Document Oriented Storage − Data is stored in the form of **__JSON__** style documents (`BSON`).
  
- **Collection**
   - Collection is a group of MongoDB documents.
   - The equivalent of an RDBMS table.
   - Collections do not enforce a schema.

- **Document**
   - Document is a set of key-value pairs.
   - Documents in a collection are of similar or related purpose.
   - Documents have `dynamic schema` OR `Schema less`  __(means that documents in the same collection do not need to have the same set of fields or structure, and common fields in a collection's documents may hold different types of data.)__.

- `RDBMS` VS `MongoDB`
 
| RDBMS         | MongoDB                          |
|---------------|----------------------------------|
| Database      | Database                         |
| Table         | Collection                       |
| Tuple/Row     | Document                         |
| column        | Field                            |
| Table Join    | Embedded Documents               |
| Primary Key   | Default key `_id`                |


# 📋 MongoDB Data Types

| Data Type               | Description                                                  | Example                                               |
|--------------------------|--------------------------------------------------------------|-------------------------------------------------------|
| **String**               | Stores text data. UTF-8 encoding is used.                    | `"name": "Omar"`                                       |
| **Integer (int32, int64)** | Stores numerical values. `int32` for 32-bit, `int64` for 64-bit integers. | `"age": 21`                   |
| **Double**               | Stores floating-point values (64-bit IEEE 754).              | `"price": 19.99`                                       |
| **Decimal128**           | Stores high-precision decimal values.                        | `"balance": NumberDecimal("1234.56")`                  |
| **Boolean**              | Stores `true` or `false`.                                    | `"isActive": true`                                     |
| **Array**                | Stores multiple values in a single field.                    | `"hobbies": ["coding", "music"]`                       |
| **Object**               | Stores embedded documents (sub-documents).                   | `"address": {"city": "Cairo", "zip": "12345"}`         |
| **ObjectId**             | Unique ID assigned to each document.                         | `"_id": ObjectId("507f1f77bcf86cd799439011")`          |
| **Date**                 | Stores date and time in UTC format.                          | `"createdAt": ISODate("2025-04-14T09:00:00Z")`         |
| **Null**                 | Stores a null value.                                         | `"deletedAt": null`                                    |
| **Binary Data (BinData)**| Stores binary data (files, images, etc.).                    | `"fileData": BinData(0, "MZ...")`                      |
| **Regular Expression**   | Stores regular expressions for pattern matching.             | `"pattern": /abc/i`                                    |
| **JavaScript**           | Stores JavaScript code.                                      | `"func": function() { return true; }`                  |
| **JavaScript with Scope**| JavaScript code with associated scope (context).             | `"func": Code("return x + y;", {"x": 1, "y": 2})`      |
| **Timestamp**            | Stores a timestamp. Mostly used internally by MongoDB.       | `"lastModified": Timestamp(1642558800, 1)`            |
| **MinKey**               | A value that compares lower than all other BSON types.       | `{ "minKey": MinKey() }`                               |
| **MaxKey**               | A value that compares higher than all other BSON types.      | `{ "maxKey": MaxKey() }`                               |

---

## 💡 Example Document

```javascript
db.dataTypesExample.insertOne({
    stringExample: "Hello, MongoDB!",
    intExample: 42,
    longExample: NumberLong("9223372036854775807"),
    doubleExample: 3.14159,
    decimalExample: NumberDecimal("1234567890.123456789"),
    booleanExample: true,
    arrayExample: ["MongoDB", "Java", "Data"],
    objectExample: {
        city: "Cairo",
        zipCode: "12345"
    },
    objectIdExample: ObjectId("507f191e810c19729de860ea"),
    dateExample: ISODate("2025-04-14T12:00:00Z"),
    nullExample: null,
    binaryExample: new BinData(0, "SGVsbG8sIE1vbmdvREEh"),
    regexExample: /Mongo/i,
    javascriptExample: function() { return "Hello from JavaScript!"; },
    javascriptWithScopeExample: new Code(
        "return x + y;", 
        { x: 10, y: 20 }
    ),
    timestampExample: Timestamp(1610000000, 1),
    minKeyExample: MinKey(),
    maxKeyExample: MaxKey()
});

___

# MongoDB Cheat Sheet 🐋
_By Omar Mohamed_

---

## 📚 Terminology

| Term         | Description                                                                                        |
|--------------|----------------------------------------------------------------------------------------------------|
| **Database** | A container for collections (similar to a database in SQL).                                         |
| **Collection** | A grouping of documents inside a database (similar to a table in SQL).                             |
| **Document** | A single record in a collection (similar to a row in SQL). It’s usually a JSON object.              |
| **Field**    | A key-value pair inside a document (similar to a column in SQL). Can store arrays, JSON objects, etc.|

---

## 💻 Basic Commands

```bash
mongosh               # Open a connection to MongoDB
show dbs              # Show all databases
use <dbname>          # Switch to a database
db                    # Show current database name
cls                   # Clear the terminal screen
show collections      # Show all collections in the current database
db.dropDatabase()     # Delete the current database
exit                  # Exit the mongosh session
```

---

## 📝 Create Operations

```javascript
db.<collectionName>.insertOne({ name: "Kyle" })
// Insert a single document

db.<collectionName>.insertMany([{ age: 26 }, { age: 20 }])
// Insert multiple documents
```

---

## 🔍 Read Operations

```javascript
db.<collectionName>.find()
// Get all documents

db.<collectionName>.find({ name: "Kyle" })
// Get all documents where name is Kyle

db.<collectionName>.find({ "address.street": "123 Main St" })
// Get all where address.street is "123 Main St"

db.<collectionName>.find({ name: "Kyle" }, { name: 1, age: 1 })
// Return only specific fields (name, age, _id)

db.<collectionName>.find({}, { age: 0 })
// Return all fields except age

db.<collectionName>.findOne({ name: "Kyle" })
// Return the first matching document

db.<collectionName>.countDocuments({ name: "Kyle" })
// Count documents matching filter
```

---

## 🔧 Update Operations

```javascript
db.<collectionName>.updateOne({ age: 20 }, { $set: { age: 21 } })
// Update first document matching filter

db.<collectionName>.updateMany({ age: 12 }, { $inc: { age: 3 } })
// Update multiple documents

db.<collectionName>.replaceOne({ age: 12 }, { age: 13 })
// Replace document entirely
```

---

## 🗑️ Delete Operations

```javascript
db.<collectionName>.deleteOne({ age: 20 })
// Delete first matching document

db.<collectionName>.deleteMany({ age: 12 })
// Delete all matching documents
```

---

## ⚙️ Complex Filter Operators

| Operator | Description | Example |
|----------|-------------|---------|
| `$eq`    | Equal to    | `db.users.find({ name: { $eq: "Kyle" } })` |
| `$ne`    | Not equal   | `db.users.find({ name: { $ne: "Kyle" } })` |
| `$gt` / `$gte` | Greater than / or equal | `db.users.find({ age: { $gt: 12 } })` |
| `$lt` / `$lte` | Less than / or equal | `db.users.find({ age: { $lt: 12 } })` |
| `$in`    | Value in array | `db.users.find({ name: { $in: ["Kyle", "Mike"] } })` |
| `$nin`   | Value not in array | `db.users.find({ name: { $nin: ["Kyle", "Mike"] } })` |
| `$and`   | All conditions must be true | `db.users.find({ $and: [{ age: 12 }, { name: "Kyle" }] })` |
| `$or`    | One of the conditions must be true | `db.users.find({ $or: [{ age: 12 }, { name: "Kyle" }] })` |
| `$not`   | Negate the condition | `db.users.find({ name: { $not: { $eq: "Kyle" } } })` |
| `$exists`| Field existence check | `db.users.find({ name: { $exists: true } })` |
| `$expr`  | Compare fields | `db.users.find({ $expr: { $gt: ["$balance", "$debt"] } })` |

---

## 🛠️ Complex Update Operators

| Operator  | Description                     | Example |
|-----------|---------------------------------|---------|
| `$set`    | Set fields                     | `db.users.updateOne({ age: 12 }, { $set: { name: "Hi" } })` |
| `$inc`    | Increment numeric fields       | `db.users.updateOne({ age: 12 }, { $inc: { age: 2 } })` |
| `$rename` | Rename fields                  | `db.users.updateMany({}, { $rename: { age: "years" } })` |
| `$unset`  | Remove fields                  | `db.users.updateOne({ age: 12 }, { $unset: { age: "" } })` |
| `$push`   | Add value to array             | `db.users.updateMany({}, { $push: { friends: "John" } })` |
| `$pull`   | Remove value from array        | `db.users.updateMany({}, { $pull: { friends: "Mike" } })` |

---

## 📟️ Read Modifiers

```javascript
db.users.find().sort({ name: 1, age: -1 })
// Sort by name (asc) and age (desc)

db.users.find().limit(2)
// Return only 2 documents

db.users.find().skip(4)
// Skip first 4 documents
```
