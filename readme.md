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
    
    - db.collection.find(query, projection)

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
$ db.recipes.find({}, { "title": 1 }).sort( {"title": 1 }).limit(2).sort();
```

2. Limit

```sh
$ db.recipes.find({}, { "title": 1 }).sort( {"title": 1 }).limit(2);
```

3. Skip

```sh
$ db.recipes.find({}, { "title": 1 }).sort( {"title": 1 }).skip(2);
```