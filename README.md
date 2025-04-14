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
