STARTING SERVER
mongod.exe

STARTING SHELL
mongo.exe

CREATING NEW DB
use cgdb	-----<ouput>----> switched to db cgdb

SHOWING DB
show dbs;

INSERT EMPTY DOCUMENT
db.cgdb.insert({})

CREATING COLLECTION
db.createCollection("employees")

CREATING DOCUMENT WITH FIELDS     INSERT FUNCTION

db.employees.insert({firstname:"aaa",lastname:"bbb"})

PRINTING DATA
db.employees.find()	//similar to select * from..//	OR    db.employees.find().pretty()
db.employees.findOne()

PRIMARY KEY
_id  field acts as primary key

COUNTING NO. OF FIELDS
db.employees.find().count()

DISPLAYING SELECTED COLUMNS
db.employees.find({},{_id:1,firstname:1})  //1 means show and 0 means hide {} means select all

UPDATE
db.employees.update({_id:3},{firstname:"Sayali"})

FOR ADDING NEW COLUMN
$set modifier
db.employees.update({firstname:"mnbv"},{$set:{salary:10000,gender:"male"}})


******if more than one documents with same name are under update command then only first document will get updates********
*********for updating documents with same data use multi:true**********
db.employees.update({lastname:"Arora"},{$set:{salary:50000}},{multi:true})

ARRAY UPDATE
db.employees.update({lastname:"Arora"},{$set:{foddILike:["Pizza","Dosa"]}})

MPDIFYING ABOYVE ARRAY
db.employees.update({lastname:"Arora"},{$push:{foddILike:"Idli"}})	//if we use [] then an array will be created inside foodILike//

UNSET
db.employees.update({lastname:"Arora"},{$unset:{foddILike:1}})

POP
db.employees.update({lastname:"Arora"},{$pop:{foddILike:1}})	//removes last element since POP operation

PULL
db.employees.update({lastname:"Arora"},{$pop:{foddILike:"Pizza"}})	//removes the element as mentioned

INC
db.employees.update({lastname:"Arora"},{$inc:{salary:2000}})	//increases salary by 2000

UPSERT 	//if existing update or insert
db.employees.update({lastname:"abcds"},{firstname:"abc",lastname:"xyz"},{upsert:true})

FIRSTNAME WITH "P"
db.employees.find({firstname:/P/})

REMOVE
db.employees.remove({firstname:/P/})

OR
db.employees.find({$or:[{firstname:"Uma"},{firstname:"Mahima"}]}).pretty()	//Uma or Mahima

AND
db.employees.find({$and:[{firstname:"Uma"},{firstname:"Mahima"}]}).pretty()	//Uma and Mahima which is blank

GREATER THAN
db.employees.find({salary:{$gt:50000}}).pretty()	//salary >50000

LEE THAN
db.employees.find({salary:{$lte:50000}},{firstname:1,salary:1}).pretty()	//salary 
<50000


LIMIT
to display limited no. of rows
db.employees.find({salary:{$lte:50000}},{firstname:1,salary:1}).pretty().limit(3)

SORT
db.employees.find({salary:{$lte:50000}},{firstname:1,salary:1}).pretty().limit(3).sort({salary:-1})

IN
db.employees.find({salary:{$in:[25000,50000]}},{firstname:1,salary:1}).pretty()

db.employees.find({$and:[{salary:{$gt:30000}},{salary:{$lt:60000}}]},{firstname:1,salary:1}).pretty()


FOR
db.employees.find().forEach(function(doc){print("Full name of emp:"+doc.firstname+"--"+doc.lastname)}).pretty()
