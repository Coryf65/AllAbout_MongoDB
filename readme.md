# All about MongoDB

- Notes for MongoDB

- Docs for MongoDB [here](https://docs.mongodb.com/ "MongoDB Documentation")

## Installing locally

- Install and Run as a Windows Service

- Run as a local user

```sh
$ mongod.exe --config mongod.cfg
```

## How to connect

- Using Compass, a tool with a GUI

- CLI

- example query

```js
// MongoDB Playground
// Use Ctrl+Space inside a snippet or a string literal to trigger completions.

// The current database to use.
use('LearningMongo');

// Search for documents in the current collection.
db.getCollection('examples')
  .find(
    {
      /*
      * Filter
      * fieldA: value or expression
      */
    },
    {
      /*
      * Projection
      * _id: 0, // exclude _id
      * fieldA: 1 // include field
      */
    }
  )
  .sort({
    /*
    * fieldA: 1 // ascending
    * fieldB: -1 // descending
    */
  });

```

## Documents and Collections

1. Documents ?

    - Field-Value Pairs
    - Stored in JSON-like BSON (Binanary JSON)
    - similar to a row in MSQL Server

2. Collectons ?

    - Grouping related Documents
    - can cap a collection to auto delete oldest data
    - not all collections need to have the same data types, and data
    - similar to tables

3. Searching for a Document

- Find()
    
    - `db.collection.find(query, projection)`

Search for any thing the contains *taco*, similar to a like in TSQL

> we are using Regex here

```sh
db.recipes.find({ "title": { $regex: /taco/i }}, { "title": 1 });
```

4. What can we store ?

-  lots of data with various types

- text, numbers, arrays, 

## Querying

- Query sent -> Cursor created -> Options and operators -> Results returned

- you can chain calls, sort of like method chaining

1. Sort

```sh
db.recipes.find({}, { "title": 1 }).sort( {"title": 1 });
```

2. Limit

```sh
db.recipes.find({}, { "title": 1 }).limit(2);
```

3. Skip

```sh
db.recipes.find({}, { "title": 1 }).skip(2);
```

### Operators and Arrays

1. `$gt` 
    - `$gt` selects those documents where the value of the field is greater than `(i.e. >)` the specified value.

2. `$lt`
    - `$lt` selects the documents where the value of the field is less than `(i.e. <)` the specified value.

3. `$lte` 
    - `$lte` selects the documents where the value of the field is less than or equal to `(i.e. <=)` the specified value.

4. `$all`
    - The `$all` operator selects the documents where the value of a field is an array that contains all the specified elements. To specify an `$all` expression, use the following prototype

5. `$in`
    - The `$in` operator selects the documents where the value of a field equals any value in the specified array. To specify an `$in` expression, use the following prototype.
    - Matches any of the values specified in an array.

> Example Get any recipe with `egg` as an ingredient.
```sh
db.recipes.find({ "ingredients.name": "egg"}, {"title": 1});
```

### Updating Documents

> Mongo also has an Upsert, update or insert

1. `$set`

    - The $set operator replaces the value of a field with the specified value.

```sh
{ $set: { <field1>: <value1>, ... } }
```

2. `$unset`

    - The $unset operator deletes a particular field. Consider the following syntax:

```sh
{ $unset: { <field1>: "", ... } }
```

3. `$inc`

    - The $inc operator increments a field by a specified value and has the following form.

```sh
{ $inc: { <field1>: <amount1>, <field2>: <amount2>, ... } }
```

### Updating Arrays

### Deleting Documents
