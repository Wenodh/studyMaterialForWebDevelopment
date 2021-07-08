## Mongodb

- use db //to create database
- db // To check your currently selected database
- db.dropDatabase()  // drop a existing database
- show dbs //check your databases list
- db.createCollection(name) / to create collection
- show collections //check the created collection
- db.tutorialspoint.insert({"name" : "tutorialspoint"}) //In MongoDB, you don't need to create collection. MongoDB creates collection automatically, when you insert some document.
- db.COLLECTION_NAME.drop()  //drop a collection from the database.
- db.COLLECTION_NAME.insert(document) //To insert data into MongoDB collection  https://www.tutorialspoint.com/mongodb/mongodb_insert_document.htm
- db.COLLECTION_NAME.insertOne(document) //to insert one document
- db.COLLECTION_NAME.insertMany(document) //to insert many document
- db.COLLECTION_NAME.find()  //To query data from MongoDB collection
- db.COLLECTION_NAME.find().pretty()  //To display the results in a formatted way
- db.mycol.findOne({title: "MongoDB Overview"}) //that returns only one document.  
- This method also accepts list of options (which are optional). Following is the list
  
![Query of Documents](https://user-images.githubusercontent.com/63317955/123526246-22414800-d6f4-11eb-9c74-0e1737f3605b.png)
	

-   db.mycol.find({ $and: [ {<key1>:<value1>}, { <key2>:<value2>} ] }) // returns if both conditions are true
-   db.mycol.find({$or: [{key1: value1}, {key2:value2}]}).pretty() // returns if any one condition is true
-   db.mycol.find({$nor: [{key1: value1}, {key2:value2}]}).pretty() // returns if values not in objects/collections
-   db.mycol.find({$NOT: [{key1: value1}, {key2:value2}]}).pretty() //To query documents based on the NOT condition
-   db.COLLECTION_NAME.update(SELECTION_CRITERIA, UPDATED_DATA) //The update() method updates the values in the existing document.
-   db.mycol.update({'title':'MongoDB Overview'},{$set:{'title':'New MongoDB Tutorial'}},{multi:true}) //By default, MongoDB will update only a single document. To update multiple documents, you need to set a parameter 'multi' to true.
-   db.COLLECTION_NAME.save({\_id:ObjectId(),NEW_DATA}) //The save() method replaces the existing document with the new document passed in the save() method
-   db.COLLECTION_NAME.findOneAndUpdate(SELECTIOIN_CRITERIA, UPDATED_DATA)
-   db.COLLECTION_NAME.updateOne(<filter>, <update>)
-   db.COLLECTION_NAME.updateMany(<filter>, <update>)
-   db.COLLECTION_NAME.remove(DELLETION_CRITTERIA) //remove all the documents meets dellition criteria
-   db.COLLECTION_NAME.remove(DELETION_CRITERIA,1) //f there are multiple records and you want to delete only the first record
-   db.mycol.remove({}) //remove all, equivalent of SQL's truncate command
-   db.COLLECTION_NAME.find({},{KEY:1}) //MongoDB's find() method, explained in MongoDB Query Document accepts second optional parameter that is list of fields that you want to retrieve. In MongoDB, when you execute find() method, then it displays all fields of a document. To limit this, you need to set a list of fields with value 1 or 0. 1 is used to show the field while 0 is used to hide the fields.
-   **\_id field is always displayed while executing find() method, if you don't want this field, then you need to set it as 0.**
-   db.COLLECTION_NAME.find().limit(NUMBER) //no of doc to show
-   db.COLLECTION_NAME.find().limit(NUMBER).skip(NUMBER) // to skip doc
-   db.COLLECTION_NAME.find().sort({KEY:1}) // 1 for acending -1 for decending
-   db.COLLECTION_NAME.createIndex({KEY:1}) // ndexes support the efficient resolution of queries. Without indexes, MongoDB must scan every document of a collection to select those documents that match the query statement. This scan is highly inefficient and require MongoDB to process a large volume of data.
- This method also accepts list of options (which are optional). Following is the list 

		
![image](https://user-images.githubusercontent.com/63317955/123527436-2c1b7900-d6fd-11eb-8dcd-9a6e72acc12a.png)
		
 
 -> Show databases
 show dbs;
 
 -> Use databases
 use local;
 
 -> Show collections
 show collections;
 
 -> Insert sample data
 db.inventory.insertMany([
     { item: "journal", qty: 25, status: "A", size: { h: 14, w: 21, uom: "cm" }, tags: [ "blank", "red" ] },
     { item: "notebook", qty: 50, status: "A", size: { h: 8.5, w: 11, uom: "in" }, tags: [ "red", "blank" ] },
     { item: "paper", qty: 10, status: "D", size: { h: 8.5, w: 11, uom: "in" }, tags: [ "red", "blank", "plain" ] },
     { item: "planner", qty: 3, status: "D", size: { h: 22.85, w: 30, uom: "cm" }, tags: [ "blank", "red" ] },
     { item: "postcard", qty: 45, status: "A", size: { h: 10, w: 15.25, uom: "cm" }, tags: [ "blue" ] }
 ]);
 
 -> Fetch documents
 db.inventory.find();
 
 -> Pretty print
 db.inventory.find().pretty();
 
 -> Filter documents
 db.inventory.find({ item: "notebook"  }).pretty();
 
 -> Show only required fields in result
 db.inventory.find({ }, { qty:1, item:1, _id: 0 }).pretty();
 db.inventory.find({ item: "notebook"  }, { qty:1, item:1, _id:0 }).pretty();
 
 -> Searching inside nested objects
 > db.inventory.find({ 'size.uom': "cm" }, { _id: 0, item: 1 }).pretty();
 
 -> Searching inside array
     -> And query
         db.inventory.find({ tags: { $all: ["blank", "plain"] } }).pretty();
     -> OR query
         db.inventory.find({ tags: { $in: ["plain", "blue"] } }).pretty();
 
 -> Operators 
    -> Greater than // $gt
         > db.inventory.find({ qty: { $gt: 25 }  }).pretty()
    -> Greater than or equal to // $gte
         > db.inventory.find({ qty: { $gte: 25 }  }).pretty()
    -> Less than // $lt
         > db.inventory.find({ qty: { $lt: 25 }  }).pretty()
    -> Less than or equal to // $lte
        > db.inventory.find({ qty: { $lte: 25 }  }).pretty()
    -> Sort
         > db.inventory.find({}, { qty: 1, item: 1, _id: 0 }).sort({ qty: -1 });
         > db.inventory.find({}, { qty: 1, item: 1, _id: 0 }).sort({ qty: 1 });
    -> Limit
         > db.inventory.find({}, { qty: 1, item: 1, _id: 0 }).sort({ qty: -1 }).limit(3);
         > db.inventory.find({}, { qty: 1, item: 1, _id: 0 }).limit(3);
    -> Skip
         > db.inventory.find({}, { qty: 1, item: 1, _id: 0 }).sort({ qty: -1 }).skip(1).limit(1);
 
 -> Updating documents
     // update 
     > db.inventory.updateOne({ item: "planner" }, { $set: { qty: 100 } });
 
     // add a field ( incase field is not the part of document )
     db.inventory.updateOne({ item: "planner" }, { $set: { price: 1000 } });
     // remove a field
     db.inventory.updateOne({ item: "planner" }, { $unset: { price: 1 } });
 
 -> Updating arrays
 db.inventory.updateOne({ item: "planner" }, { $push: { tags: "magenta" } });
 db.inventory.updateOne({ item: "planner" }, { $pull: { tags: "blank" } });
 
 -> Inserting single document
 db.inventory.insertOne({ item: "diary", qty: 25, status: "A", size: { h: 14, w: 21, uom: "cm" }, tags: [ "blank", "red" ] });
 
 -> Deleting documents
 > db.inventory.deleteOne({ item: "diary" });
 
 -> Indexes
 > db.inventory.getIndexes();
 > db.inventory.find({item: "planner"}).explain("executionStats");
 > db.inventory.createIndex({ item: 1 });
 > db.inventory.dropIndex({ item: 1});
 
 -> Drop collection
 > db.inventory.drop();


	
[Nodejs and mongodb](https://www.js-tutorials.com/nodejs-tutorial/crud-operations-using-nodejs-express-mongodb-mongoose/)
 

