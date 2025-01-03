## MONGO DB

- a NoSQL management system that manange HuMONGOus amount of data
- general idea is that data is access is stored together in a document in BSON

### TERMINOLOGIES

1. DOCUMENT
   - a group of field value pairs that represent an obj
2. COLLECTION
   - group of 1 or more document
3. DATABASE
   - a group of 1 or more collection

### INSTALLATION

1. [MongoDB](https://www.mongodb.com/try/download/community) (checked **compass**, and **install as service**)
2. [MongoDB Shell](https://www.mongodb.com/try/download/shell)
   - you might need to copy executable, if so. just open the extracted zip, go to `bin`, right click `mongoDB.exe`, open `properties` and copy the `Location`

### ESTABLISHING CONNECTION

- open the mongo executable inside the `MERN` folder and type

```js
mongosh;
//establish connection
```

### vscode and mongo

- you can establish a connection in mongodb using an extension

### HOW TO NAVIGATE

- this are all possible using mongodb compass

#### `show dbs`

- shows all the database in the file

#### `use nameofdbs`

- can be used to create or navigate a dbs

#### `db.createCollection("nameofthecollection")`

- creates a collection

```bash
db.createCollection("students")
```

#### `db.dropDatabase();`

- removes a database, this function is used id you are in the file na

**or use all of this inside the mongodb compass**

#### `db.nameofcollection.insertOne({contains the value woth many fields/obj as you need})`

- inserts a document in a collection

```bash
db.debtors.insertOne({name:"Klay", contact: "", totalBalance: 0, debts: []})
```

#### `db.nameofcollection.find()`

- navigrates through that collection to see what it has

#### `db.nameofcollection.insertMany({}, {}, {})`

```bash
db.debtors.insertMany([{name:"Klay", contact: "", totalBalance: 0, debts: []}, {name:"Mynel", contact: "", totalBalance: 0, debts: []}, {name:"Andrei", contact: "", totalBalance: 0, debts: []}])
```

#### `db.nameofcollection.find().sort({fieldtosort})`

- `string: 1` - sort in alphabetical order
- `string: -1` - sort in reverse alphabetical order
- `integer/bollean: 1` - sorts in ascending value
- `integer/bollean: -1` - sorts in descending value

#### `db.nameofcollection.find().limit(numberofdocumentyouwanttobereturn)`

- you can combine `sort()` and `limit()`

#### `db.nameofcollection.find({query}, {projection})`

```js
db.debtors.find({ name: "Aceron" });
//returns all document that has Aceron as the name
```

```js
db.debtors.find({}, { debt: true });

//returns all the document but only the debt
```

#### `db.nameofcollection.updateOne(filter, update)`

- updates the database, by default use the \_id as the filter to accurately change or update

```js
db.students.updateOne(
  { name: "Klay" },
  { $set: { contact: "clarencekiethdelacruz@gmail.com" } }
);

//updates the contact
```

```js
db.students.updateOne({ name: "Klay" }, { $unset: { contact: "" } });

//removes the contact field
```

#### `db.nameofcollection.updateMany(filter, update)`

- does the samething but edits more than one document, depending on ur filter

```js
 db.debtors.updateMany(contact: {$exists: false}, {$set:{contact: "NA"}})
 //looks if contact exists on if it doesnt on a document it'll create one
```

#### `db.nameofcollection.deleteOne(filter)`

- deletes a document

```js
db.debtors.deleteOne({ name: "Klay" });
//deletes a document that has a Klay in its name
```

#### `db.nameofcollection.deleteMany(filter)`

- deletes many document

```js
db.debtors.deleteMany({debt: []})
//deletes documents that doesnt have a debt or an empty array in the debt field

 db.debtors.deleteMany(contact: {$exists: false})
 //looks if contact exists on if it doesnt it will delete all documents
```

### COMPARISON OPERATORS

- denoted by a `$`. Returns data based on value comparisons

#### `$ne`

- return a document not equal to the filter

#### `$lt`

- returns a document thats less than to the filter

#### `$lte`

- returns a document thats less than or equal to the filter

#### `$gt`

- returns a document thats greater than to the filter

#### `$gte`

- returns a document thats greater than or equal to the filter

#### `$in`

- returns a document thats contain multiple filters on one field

```shell
db.debtors.find({name: {$in: "Klay", "Aceron", "Andrei"}})
```

#### `$nin`

- returns a document thats does not contain multiple filters on one field

```shell
db.debtors.find({name: {$nin: "Klay", "Aceron", "Andrei"}})
```

### LOGICAL OPERATORS

- returns data based on expressions that evaluates to true or false

#### `$and`

- returns the value if all conditions is true

```shell
db.debtors.find({$and:[{name: "Klay"}, {contact: ""}])
```

#### `$or`

- returns a value if atleast one of the conditions is true

#### `$nor`

- returns a value if all conditions is false

#### `$nor`

- returns a value if all conditions is false

#### `$not`

- returns a value opposites to your condition

### INDEXES

```js
db.debtors.find({ name: "Klay" }).explain("executionStats");
//gives the executions stats of that querry
```

#### `db.debtors.createIndex({name: 1})`
