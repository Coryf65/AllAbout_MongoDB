# All about MongoDB

- Notes for MongoDB

- Docs for MongoDB [here](https://docs.mongodb.com/ "MongoDB Documentation")

- If you have used a Relational SQL DB concepts and terms, see the terminology comparison [here](https://docs.mongodb.com/manual/reference/sql-comparison/)

- No Locks or Transactions

## About MongoDB

> MongoDB stores data in flexible, JSON-like documents, meaning fields can vary from document to document and data structure can be changed over time
>
>The document model maps to the objects in your application code, making data easy to work with
>
>Ad hoc queries, indexing, and real time aggregation provide powerful ways to access and analyze your data
>
>MongoDB is a distributed database at its core, so high availability, horizontal scaling, and geographic distribution are built in and easy to use
>
>MongoDB is free to use. Versions released prior to October 16, 2018 are published under the AGPL. All versions released after October 16, 2018, including patch fixes for prior versions, are published under the Server Side Public License (SSPL) v1.
>
>` from: MongoDB Official Website` [here](https://www.mongodb.com/what-is-mongodb) 

## Installing locally

- Install and Run as a Windows Service (suggested way, easier)

- Run as a local user

```sh
$ mongod.exe --config mongod.cfg
```

## How to connect

- Using Compass, a tool with a GUI

- CLI

- VSCode Mongo Extension : [VS Marketplace Link](https://marketplace.visualstudio.com/items?itemName=mongodb.mongodb-vscode)

> example query, connected using VSCode

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

> Mongo also uses an Upsert, update or insert

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

1. `$push`
    
    - The $push operator appends a specified value to an array.
    
> The $push operator has the form:

```sh
{ $push: { <field1>: <value1>, ... } }
```

2. `$pull`
    
    - The $pull operator removes from an existing array all instances of a value or values that match a specified condition.

> The $pull operator has the form:

```sh
{ $pull: { <field1>: <value|condition>, <field2>: <value|condition>, ... } }
```


### Deleting Documents

1. `db.collection.deleteOne()`
    - Delete at most a single document that match a specified filter even though multiple documents may match the specified filter.
    > New in version 3.2.

2. `db.collection.deleteMany()`
    - Delete all documents that match a specified filter.
    > New in version 3.2.

3. `db.collection.remove()`
    - Delete a single document or all documents that match a specified filter.


## Data Modeling and Schema

    "Data that is accessed together should be stored together." - MongoDB

 - One to One

    - We would want to generally store the ingredients in the recipes, or
    store the address in the users

- One to Many

    - one recipe to many comments
    - example have a recipe with the top 3 comments and have a load
    more button that will load an all comments from another documents

- we do have some gotchas,

    - Will your data change ?
    - Can you store some of your data ?

## Indexes / Indecies

Compound indexes, regular indexes, and geo-spatial indexes

- See our indexes

    - `db.recipes.getIndexes()` or `db.recipes.getIndicies()`

- create an index

    - create an index based in cook_time asc
    - `db.recipes.createIndex({"cook_time" : 1})`

- remove and index, need the name of a index

    - `db.recipes.dropIndex("cook_time_1");`

