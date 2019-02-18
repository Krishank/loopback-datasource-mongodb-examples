
# Loopback DataSource Example


This project contains the steps how to setup a loopback project using mongo db


## Prerequisite

  
```

node > 6

npm > 3

MongoDB > 4

loopback cli

```

  

- First install Loopback CLI to create project:

```
npm install -g loopback-cli
```

- Install Mongo DB

  

```
brew install mongo
brew services start mongodb
```

- Check Mongo DB is running in which port

  

```
lsof -i | grep mongo
```

  

- Create Project via loopback cli run the below command and answer the questions asked by cli [Documentation](https://loopback.io/doc/en/lb2/Create-a-simple-API.html)

```
lb loopback

Which version of LoopBack would you like to use?
select 3.x

What kind of application do you have in mind?
select notes

Switch to your project: cd <yourProject>

Run Project: node .
```

  

- Now create datasource via cli and answer the questions asked by cli to create datasource

  

```
create datasourc: lb datasource

? Enter the datasource name: myMongo
? Select the connector for myMongo: MongoDB (supported by StrongLoop)
? Connection String url to override other settings (eg: mongodb://username:password@hostname:port/database):
? host: localhost
? port: 27017
? user:
? password: [hidden]
? database: noteDB
? Install loopback-connector-mongodb@^4.0.0 Yes

Now you datasource.json (./server/datasource.json) should look like this 

{  
	"db":{  
		"name":"db",  
		"connector":"memory"  
	},  
	"myMongo":{  
		"host":"localhost",  
		"port":27017,  
		"url":"",  
		"database":"noteDB",  
		"password":"",  
		"name":"myMongo",  
		"user":"",  
		"connector":"mongodb"  
	}  
}
 
```

  

- Map your modal to collection (common/models/note.json)

 
```
"options": {
	"validateUpsert": true,
	"mongodb": {
		"collection": "notesData"
	}
},

```

  

- Map your modal to datasource (./server/model-config.json)

  

```

"Note": {
"dataSource": "myMongo" // your datasource name (./server/datasources.json)
}
```

  
  

Basic Mongo Commands

  

```
Install: brew install mongo

Find Host: lsof -i | grep mongo

Start: brew services start mongodb

Connect to Mongo: mongo mongodb://localhost:27017

Show all dbs: show dbs

use existing or create db: use <dbName>

Find Collection Inside db: db.notesData.find()
```