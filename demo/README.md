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


## queries

>to use `MONGOSH` (shell in compass)
>![Click mongosh](./img/open_mongosh.png)
>
>
>```javascript
>use <database_name> (demo)
>```
>
- Show feature for search history

### single field
- 

-
```javascript
db.airbnb.find({_id: "10006546"})
db.airbnb.find({_id: "10006546"}, {description: 1})
```


### multiple fields (compound index)

### covered query

### wildcard index
- create on amenities 
- query TV
- query TV and Washer
- add new field to amenities (Beer)
- query for it (with explain)
