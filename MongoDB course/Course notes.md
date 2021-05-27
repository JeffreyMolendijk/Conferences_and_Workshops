# MongoDB - The Complete Developer's Guide 2021

## Installing MongoDB (lecture 7)
Install MongoDB community edition and the database tools on Windows, following the instructions found here: https://docs.mongodb.com/database-tools/installation/installation/ . 
Both the MongoDB folder and database tools bin folders need to be added to the Path variable. Confirm that the tools have been added by running `mongo` and `mongoimport` in your cmd. 

<br>

## Getting started (lecture 9)
Start mongoDB by typing `mongo` and type `show dbs` to show your current databases. You can switch to a database, even if it does not exist yet (e.g. `use shop`). We can then start adding data as well. When inserting data, the keyname does not need quotes, as these will be added in the background automatically (but it's good practice to add them). 

```
use shop
db.products.insertOne({"name": "Book", "price": 12.99})
```

We can now look at the stored data by using the find command, and can also add the pretty command for a nicer output format. 

```
db.products.find()
db.products.find().pretty()
```

We can add some more data, with the same keys, or even new ones (description). We can even add nested data (details containing both CPU and memory).

```
db.products.insertOne({"name": "Chair", "price": 149.99})
db.products.insertOne({"name": "Desk", "price": 200, "description": "This is a desk!"})
db.products.insertOne({"name": "Desk", "price": 200, "description": "This is a desk!", "details": {"CPU": "Intel i7", "memory": 32}})
```

<br>


## Understanding databases, collections and documents (lecture 15)
You server typically contains a database, which can contain multiple collections (like a table in a SQL database). Each collection can contain many documents, which are different pieces of data. Databases, collections and documents are created automatically (implicitly) in MongoDB when you start working with data. But we can also manually (explicitly) create these.

## Creating Databases and Collections (lecture 17, 18 & 19)
Databases are created by running the `use` command, followed by inserting some data (otherwise it is not saved). Similarly, we can start referring to a collection in a database that doesn't exist yet, that will be created once we enter data. When we enter data into MongoDB, it will give you a message with an ObjectID. When we look at our data (using `find`) we actually see that the first entry is the ID. The data we enter here is actually the JSON format, but MongoDB internally converts it to Binary data (BSON)! BSON takes less space, and allows some extra datatypes to be added that are not possible in JSON (e.g. the _id tag is not valid JSON).

```
use flights
db.flightData.insertOne({
    "departureAirport": "MUC",
    "arrivalAirport": "SFO",
    "aircraft": "Airbus A380",
    "distance": 12000,
    "intercontinental": true
  })
  db.flightData.find().pretty()
```

## CRUD operations (lecture 20)
Below are the commonly used CRUD operations:

Create
* insertOne(data, options)
* insertMany(data, options)

Read
* find(filter, options)
* findOne(filter, options)

Update
* updateOne(filter, data, options)
* updateMany(filter, data, options)
* replaceOne(filter, data ,options)

Delete
* deleteOne(filter, options)
* deleteMany(filter, options)

## Finding, inserting, deleting and updating (lecture 21, 22 & 23)
We can delete data using `deleteOne` and have to give it a keypair to delete. This command will only delete the first entry that matches. Running this command will acknowledge, and tell you how many documents have been deleted. (*Note, the whole object that matches is deleted, not just that keypair). `deleteMany` can delete many documents, that share a keypair. The `updateOne` command is used to add new entries to an existing collection. This command requires a filter (document with distance of 12000) and an update, indicated by the $set parameter. If that key (marker) already exists, it will be updated, otherwise a new key will be added. If we would want to add something to all documents, we could use `updateMany` with empty curly braces as the filter! This also works with `deleteMany`. `insertMany` is used to add multiple documents in one command. We can use the find command with different types of filters as well, including greater than ($gt).

```
show dbs
use flights
db.flightData.find()
db.flightData.deleteOne({departureAirport: "TXL"})
db.flightData.updateOne({distance: 12000}, {$set: {"marker": "delete"}})
db.flightData.updateMany({}, {$set: {"marker": "toDelete"}})
db.flightdata.insertMany([
  {
    "departureAirport": "MUC",
    "arrivalAirport": "SFO",
    "aircraft": "Airbus A380",
    "distance": 12000,
    "intercontinental": true
  },
  {
    "departureAirport": "LHR",
    "arrivalAirport": "TXL",
    "aircraft": "Airbus A320",
    "distance": 950,
    "intercontinental": false
  }
]
)
db.flightData.find({distance: 12000})
db.flightData.find({distance: {$gt: 1200}})

```