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
