# Instructions for the database 

## Setup
- Install [Compass](https://docs.mongodb.com/compass/master/install/)
- Install [MongoDB](https://docs.mongodb.com/manual/administration/install-community/)

## Prepare
- Download from https://github.com/neelabalan/mongodb-sample-dataset/blob/main/sample_airbnb/listingsAndReviews.json
- Start MongoDB
- Start Compass and connect to `localhost` 
- ![Click Fill connection string button](./img/localhost_overview.png) Click `fill in ..` 
- ![Window to set connection string values](./img/localhost_fill_connection_string.png)  Click `connect`
- ![Create new database to import data](./img/create_database.png)
- I will use: 
  - database: `demo`
  - collection: `airbnb`
- ![Select collection](./img/select_collection.png)
- Click `add data`, `import file` and choose `json` and enter path to the previous downloaded `json` file

> [Guide to sample data](https://docs.atlas.mongodb.com/sample-data/sample-airbnb/)

## queries
>to use `MONGOSH` (shell in compass)
>![Click mongosh](./img/open_mongosh.png)

>```javascript
>use <database_name> (demo)
>```

- [Compass Guide for queries](https://docs.mongodb.com/compass/current/query/filter/)
- Show feature for [search history](https://docs.mongodb.com/compass/master/query/queries/)
- [Explain results](https://docs.mongodb.com/manual/reference/explain-results/)

### single field index
> [Docs](https://docs.mongodb.com/manual/core/index-single/)

```javascript
db.airbnb.find({_id: "10006546"}) //IDHACK
db.airbnb.find({_id: "10006546"}, {description: 1}) //PROJECTION DEFAULT
db.airbnb.find({property_type: "House"}) //COLLSCAN
```

### multiple fields (compound index)
> [Docs](https://docs.mongodb.com/manual/core/index-compound/)

```javascript
db.airbnb.find({property_type : "House", bedrooms : {$gt : 3}, {reviews : 0, amenities: 0}})
db.airbnb.find({property_type : "House", bedrooms : {$gt : 3}, cancellation_policy : {$in : ["moderate", "flexible"]}}, {reviews : 0, amenities: 0})
db.explain. ...
```

- create index on all fields of query
- repeat last query with explain after index creation
- repeat second last query with explain

```javascript
db.airbnb.find({cancellation_policy : "moderate"})
db.airbnb.explain().find({property_type : "House", cancellation_policy : {$in : ["moderate", "flexible"]}})
```
> Since a query on item and stock omits the location index prefix, it cannot use the stock index field which follows location. Only the item field in the index can support this query. See Create Indexes to Support Your Queries for more information.

### covered query
> [Docs](https://docs.mongodb.com/manual/core/query-optimization/#std-label-read-operations-covered-query)

### wildcard index
> [Docs](https://docs.mongodb.com/manual/core/index-wildcard/) 
- query against fields whose names cannot be known in advance
- only single field
> [Create Wildcard Index in compass](https://docs.mongodb.com/compass/master/indexes/#std-label-compass-wildcard-index)

- create on amenities 
- query TV
- query TV and Washer
- add new field tbaby shao amenities (Beer)
- query for it (with explain)
