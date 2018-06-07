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
  "database": "admin",
  "password": "user_password",
  "tenant": "my_default_tenant",
  "prefix": "tenant_prefix_",
  "name": "mydb",
  "user": "user_with_root_role",
  "connector": "mongodb-mt"
}
```
PS:
  * User requires the root role in mongodb.
  * Tenant is the default tenant to connect if AccessToken not constains a tenant.
  * Prefix is the tenant prefix, this is concatenate with tenant like this: settings.prefix + settings.tenant.

## Change tenant

Tenant changes with AccessToken custom attribute named "tenant".
When user request with accesss 