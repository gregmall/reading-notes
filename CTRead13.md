# Aggregation Pipeline
* the aggregation pipeline is a framework for data aggregation modeled on the concept of data processing pipelines
## Pipeline
- MongoDB aggregation pipeline consists of stages.
  - each stage transforms the documents as they pass through the pipeline
  - stages do not need to produce one output document for every input document
## Pipeline Expressions
- Pipeline expressions specify the transformation to apply to the input documents.
- expressions are stateless with one exception: accumulator expressions
## Aggregation Pipeline Behavior
* the aggregate command operates on a single collection, passing the entire collection into the aggregation pipeline
* optimize using the following strategies:
### **Pipeline Operators and Indexes**
**$match**

  -The *$match* stage can use an index to filter documents if it occurs at the beginning of a pipeline.

**$sort**
  - The *$sort* stage can use an index as long as it is not preceded by a *$project*, *$unwind*, or *$group* stage.

**$group**
  - The *$group* stage can sometimes use an index to find the first document in each group if all of the following criteria are met:

      - The *$group* stage is preceded by a *$sort* stage that sorts the field to group by,
      - There is an index on the grouped field which matches the sort order and
      - The only accumulator used in the *$group* stage is $first.

**$geoNear**
  - The *$geoNear* pipeline operator takes advantage of a geospatial index. When using *$geoNear*, the *$geoNear* pipeline operation must appear as the first stage in an aggregation pipeline.

### **Early Filtering**
* use the *$match*, *$limit*, and *$skip* stages to restrict the documents that enter at the beginning of the pipeline

## Considerations

### **Sharded Collections**
* aggregation pipeline supports operations on sharded collections
### **Aggregation Pipeline vs Map-Reduce**
* Various map-reduce operations can be rewritten using aggregation pipeline operators, such as *$group*, *$merge*, etc.
### **Limitations**
* Aggregation pipeline have some limitations on value types and result size
### **Pipeline Optimization**
* The aggregation pipeline has an internal optimization phase that provides improved performance for certain sequences of operators

# Aggregations in MongoDB by Example
## Starting an Aggregation Pipeline
```
{
  "id": "1",
  "firstName": "Jane",
  "lastName": "Doe",
  "phoneNumber": "555-555-1212",
  "city": "Beverly Hills",
  "state: "CA",
  "zip": 90210
  "email": "Jane.Doe@compose.io"
}
```
* we call the aggregate funtion on the customer's collection:
```
> db.customers.aggregate([ ... aggregation steps go here ...]);
```
* The **aggregate** function accepts an array of data transformations which are applied to the data in the order they are defined.
  - makes aggregation like other data flow pipelines

## Matching Documents
* The matching expression looks and acts much like the MongoDB find function or a SQL **WHERE** clause
```
> db.customers.aggregate([ 
  { $match: { "zip": 90210 }}
]);
```
* Using the match stage in this way is no different from using the find method on a collection
## Grouping Documents
* after filtering we can start grouping together documents we want into useful subsets:
```
> db.customers.aggregate([ 
  { $match: {"zip": "90210"}}, 
  { 
    $group: {
      _id: null, 
      count: {
        $sum: 1
      }
    }
  }
]);
```
* The **$group** transformation allows us to group documents together and performs transformations or operations across all of those grouped documents. 
## Gaining Insights with Sum, Min, Max, and Avg
* transaction model follows:
```
{
  "id": "1",
  "productId": "1",
  "customerId": "1",
  "amount": 20.00,
  "transactionDate": ISODate("2017-02-23T15:25:56.314Z")
}
```
* calculate total sales made in january:
```
{
   $match: {
    transactionDate: {
        $gte: ISODate("2017-01-01T00:00:00.000Z"),
        $lt: ISODate("2017-02-01T00:00:00.000Z")
    }
  }
}
```
* The **$gte** and **$lt** operators are comparators that allow us to limit our dates to specific range
* The next stage of the pipeline is summing the transaction amounts and putting that amount in a new field called total:
```
{
  $group: {
    _id: null, 
    total: {
      $sum: "$amount"
    }
  }
}
```
* final query looks like this:
```
> db.transactions.aggregate([
  { 
    $match: {
      transactionDate: {
        $gte: ISODate("2017-01-01T00:00:00.000Z"),
        $lt: ISODate("2017-01-31T23:59:59.000Z")
      }    
    }
  }, {
    $group: {
      _id: null,
      total: {
        $sum: "$amount"
      }
    }
  }
]);
```
* Combined with the **$match** statement it looks like this:
```
> db.transactions.aggregate([
  { 
    $match: {
      transactionDate: {
        $gte: ISODate("2017-01-01T00:00:00.000Z"),
        $lt: ISODate("2017-01-31T23:59:59.000Z")
      }    
    }
  }, {
    $group: {
      _id: null,
      total: {
        $sum: "$amount"
      },
      average_transaction_amount: {
        $avg: "$amount"
      },
      min_transaction_amount: {
        $min: "$amount"
      },
      max_transaction_amount: {
        $max: "$amount"
      }
    }
  }
]);
```
* the final gives us a picture of monthly sales:
```
{ 
  _id: null, 
  total: 20333.00, 
  average_transaction_amount: 8.50,
  min_transaction_amount: 2.99,
  max_transaction_amount: 347.22
}
```
