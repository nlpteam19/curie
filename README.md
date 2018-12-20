# Curie
This repository contains three datasets which are described in our paper **"Natural Language Question Answering over BI data using a Pipeline of Multiple Sequence tagging Networks"**.


## WikiSQL dataset :
In this paper we present a novel approach to parse the natural language sentence into an intermediate sketch which is basically a low level interpretation of the nl sentence. We identify the n-grams (uni, bi, tri, etc.) in the sentences which could be a column, value (entity) or aggregation (if applied). We use the sequence tagging technique to train the network. Since original [WikiSQL dataset](https://github.com/salesforce/WikiSQL) is not annotated like the way our models are trained, we present the annotated data `wikidataset.zip` in the following format which could be used in many other applications:

### Format
```json
  {
    "phase":1,
    "question":"who is the player that wears number 42?",
    "sql":{
          "conds":[
             [
                0,
                0,
                "42"
             ]
          ],
          "sel":0,
          "agg":0
       },
     "table_id":"1-10015132-11",
     "annotations":{
                   "predicate":{
                               "input": 
                                 [
                                   "who", "is", "the", "player", "that", "wears", "number", "42"
                                 ], 
                               "output": 
                                 [
                                   "o", "o", "o", "a", "o", "o", "o", "o"
                                 ]
                    }, 
                    "value":{
                            "input": 
                                [
                                  "who", "is", "the", "<attr>", "that", "wears", "number", "42"
                                ], 
                             "output": 
                                [
                                  "o", "o", "o", "o", "o", "o", "o", "a"
                                ]
                    }, 
                    "aggregation":{
                                  "input": 
                                    [
                                      "who", "is", "the", "<attr>", "that", "wears", "number", "<val>"
                                    ],
                                  "output": 
                                    [
                                      "o", "o", "o", "o", "o", "o", "o", "="
                                    ]
                   }
      }
    }

```
          
The fields represent the following:

- `annotations`: the annotations contains three fields for predicate, value and aggregation.
  - `predicate`: this represents the select part for the SQL. The indexes where **tag [a]** occurs in output represents the hint for the `select` column.
  - `value`: this represents the value part (where) for the SQL. The indexes where [a,b,c,d..] occurs in output represents the value present.
  - `aggregation & operators`: the `predicates` are replaced with `<attr>` tag and values are replaced with `<val>` tags in the inout. Any aggregation (like count, sum, min, max) is present at the <attr> index in the output and operators (like =, >=, <=, >) would be marked at <val> index.
          
## Enterprise Dataset 1 (related to employees and their allocation data)
This data cannot be shared publicly but schema is present in `ent1_dataset.json` 

## Enterprise Dataset 2 (related to pharmaceutical domain)
This data cannot be shared publicly but schema is present in `ent2_dataset.json`
