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


# 📋 MongoDB Data Types Cheat Sheet

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
