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

