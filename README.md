# loopback-connector-mongodb-mt

A simple solution to use multitenant with MongoDB.
This package is a fork from official MongoDB connector for the LoopBack framework.

Please see the full official documentation at [loopback-connector-mongodb](https://github.com/strongloop/loopback-connector-mongodb).

## Installation

In your application root directory, enter this command to install the connector:

```sh
npm install loopback-connector-mongodb-mt --save
```

This installs the module from npm and adds it as a dependency to the application's `package.json` file.

If you create a MongoDB data source using the data source generator as described below, you don't have to do this, since the generator will run `npm install` for you.

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
  "tenantPrefix": "tenant_prefix_",
  "name": "mydb",
  "user": "user_with_root_role",
  "authSource" : "admin",
  "connector": "mongodb-mt"
}
```
PS:
  * User requires the root role in mongodb.
  * Tenant is the default tenant to connect if AccessToken not constains a tenant.
  * TenantPrefix is the tenant prefix, this is concatenate with tenant like this: settings.tenantPrefix + settings.tenant.

## Change tenant

Tenant changes with AccessToken custom attribute named `tenant`.
When user request with accesss.

## Model methods

Use tenant with model methods require the AccessToken object in options of the method like this:

```javascript
Model.find({where:{}}, {accessToken}, (err, instances) => {
  // ...
});

instance.save({accessToken}, (err) => {
  // ...
});
```

## Autoupdate and Automigrate

Get the attribute connector of the datasource and call the method with AccessToken like:

```javascript
dataSource.connector.autoupdate(myModelName, {accessToken}, (err) => {
  // ...
});

dataSource.connector.automigrate(myModelName, {accessToken}, (err) => {
  // ...
});
```
