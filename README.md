# studyMaterialForWebDevelopment
what is git and github?


**Html**

**Css**

- [centering-css-complete-guide](https://css-tricks.com/centering-css-complete-guide/)

**javaScript**
dom manupulation?
asyncronus?

what is chrome extension?

1.what is object
<details>
object is one of the data type in javascipt
The Object class represents one of JavaScript's data types. It is used to store various keyed collections and more complex entities. Objects can be created using the Object() constructor or the object initializer / literal syntax.
Description

Nearly all objects in JavaScript are instances of Object; a typical object inherits properties (including methods) from Object.prototype, although these properties may be shadowed (a.k.a. overridden). However, an Object may be deliberately created for which this is not true (e.g. by Object.create(null)), or it may be altered so that this is no longer true (e.g. with Object.setPrototypeOf).

Changes to the Object prototype object are seen by all objects through prototype chaining, unless the properties and methods subject to those changes are overridden further along the prototype chain. This provides a very powerful although potentially dangerous mechanism to override or extend object behavior.

The Object constructor creates an object wrapper for the given value.

    If the value is null or undefined, it will create and return an empty object.
    Otherwise, it will return an object of a Type that corresponds to the given value.
    If the value is an object already, it will return the value.

When called in a non-constructor context, Object behaves identically to new Object().
  [click for in detail](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)
</details>

constructor?
instance?
this?
oop?
functional programming?
 System Design and Scalability.
Hackerothons
<p>Mongadb</p>
<details>
    
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
    
![Query of Documents](https://user-images.githubusercontent.com/63317955/123526246-22414800-d6f4-11eb-9c74-0e1737f3605b.png)

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
 
</details>
Database
Api calls

 
 **regExp**
   - [introduction to regexp](https://www.w3schools.com/js/js_regexp.asp)
   - [cheet sheet](https://www.w3schools.com/jsref/jsref_obj_regexp.asp)
 
    
## Books
-[Learning JavaScript Design Patterns](https://addyosmani.com/resources/essentialjsdesignpatterns/book/)
-[basic tutorials on js and phython](https://edabit.com/tutorials)
-[almost every document available](https://devdocs.io/)
## Videos
   - [Learn Javascript in 12 minutes](https://www.youtube.com/watch?v=Ukg_U3CnJWI)
   - [Javascript Algorithms and Data Structures](https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/basic-javascript/)
## links
   - [Javascript Algorithms With Explanations](https://github.com/trekhleb/javascript-algorithms)
   - [entire-freecodecamp-curriculum](https://www.freecodecamp.org/news/i-completed-the-entire-freecodecamp-curriculum-in-a-month-while-recording-everything/)

