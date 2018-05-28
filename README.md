# loopback-connector-mongodb-mt

A simple solution to use multitenant with MongoDB.
This package is a fork from official MongoDB connector for the LoopBack framework.

Please see the full official documentation at [loopback-connector-mongodb](https://github.com/strongloop/loopback-connector-mongodb).

## Installation

In your application root directory, enter this command to install the connector:

```sh
npm install loopback-connector-mongodb-mt --save
```

## Creating a MongoDB data source

Use the [Data source generator](http://loopback.io/doc/en/lb3/Data-source-generator.html) to add a MongoDB data source to your application.  
The generator will prompt for the database server hostname, port, and other settings
required to connect to a MongoDB database.  It will also run the `npm install` command above for you.

The entry in the application's `/server/datasources.json` will look like this:

```javascript
"mydb": {
  "host": "myserver",
  "port": 27017,
  "url":  "",
  "database": "test",
  "password": "mypassword",
  "name": "mydb",
  "user": "me",
  "connector": "mongodb-mt"  
}
```

## Change tenant

Tenant changes with AccessToken custom attribute named "tenant".
When user request with accesss 