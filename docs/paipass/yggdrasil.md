## Yggdrasil 

The primary concepts you will likely be using to submit data will be contained in an extension of the initial PDP2 code called Yggdrasil. 

Yggdrasil was designed s.t. a user could submit data to PAI Pass in a repeated way. The data is structured arbitrarily by the Schema + Field ORM. The Data Field Type helps inform the backend in how to store this data as well as inform the frontend on what kind of data it is receiving. The share group determines who has access to this data. A Dataset is an instance of a Schema. A "Data" is an instance of a Field. 

### Schema

A Schema functions to structure the data. It has a name, an owner, share group, and is composed of an arbitrary number of fields.

### Field

A Field functions to define what kind of Data a Schema will hold at that particular section of the Schema. It has a a name, a type, and a group. The group functions to show if its parent is the Schema or another Field.  

### Field Data Type

There are about 8 recognized data types for Yggdrasil. They can be grouped into 3 separate classes: Objects, Lists and Primitives. Objects provide a mapping to other data types. Lists provide a sequence of data types. Primitives include: Text, Dates, Files, Images, Videos, and Integers. There is a distinction between Files and Images and Videos so that a frontend that is utilizing this may link to them s.t. they are displayed appropriately as Images and Videos to the user. In fact, all primitives are used to help the corresponding frontend display them appropriately.  

### Share Group

### Dataset

A Dataset is an instance of a Schema. That is, it is created when a set of data is "submitted" to a given schema.  

### Data



### Example Dataset

```json
{
  "count": 5,
  "field1": {
    "fieldType": "PRIMITIVE",
    "name": "title",
    "selectedFieldType": "Text"
  },
  "field2": {
    "count": 1,
    "field1": {
      "fieldType": "PRIMITIVE",
      "name": "ingredient",
      "selectedFieldType": "Text"
    },
    "fieldType": "LIST",
    "name": "ingredients"
  },
  "field3": {
    "fieldType": "PRIMITIVE",
    "name": "primaryImage",
    "selectedFieldType": "Text"
  },
  "field4": {
    "count": 1,
    "field1": {
      "fieldType": "PRIMITIVE",
      "name": "Property",
      "selectedFieldType": "Text"
    },
    "fieldType": "LIST",
    "name": "Verified Properties"
  },
  "field5": {
    "count": 1,
    "field1": {
      "count": 2,
      "field1": {
        "fieldType": "PRIMITIVE",
        "name": "Event Name",
        "selectedFieldType": "Text"
      },
      "field2": {
        "fieldType": "PRIMITIVE",
        "name": "Timestamp",
        "selectedFieldType": "Date"
      },
      "fieldType": "OBJECT",
      "name": "Timeline Event"
    },
    "fieldType": "LIST",
    "name": "Timeline Events"
  },
  "name": "20200808supplychain"
}
```


## REST API




## Internals

In essence a method, in one of the views creates a __SubmitUserData__ instance by passing it a user or PDP2Subscription instance. That instance's \_\_call__ function is then called with or without a configuration or json dataset. This \_\_call__ function then tries to fill in missing details. 

In the first iteration of this, there was no concept of arbitrary data that the user could submit. That is, the user merely had profile data and when any of that changed, the entire user profile was resubmitted to the blockchain. Thus, the __json_data__ parameter could be left as __None__ and this functor would submit the user profile associated with what was passed in the constructor of __SubmitUserData__.
 
 As [Yggdrasil](https://github.com/projectpai/paipass/tree/main/backend/yggdrasil) grew, this came to encompass arbitrary data submitted by the user. Since there can be an arbitrary amount of arbitrary data, it no longer made sense to submit every piece of data associated with the user. Thus we added the __json_data__ parameter to submit a user's arbitrary data (whether it be on the initial data creation or when the data is modified).
 
This work has largely been an evolutionary process whereby new functionality has been added on in an ad-hoc manner that largely
 defies more typical software engineering processes; where you might expect modularity and a strong separation of concerns you will find strong coupling. 

### Source Code

The source code can largely be found across three files; here,

[paipass/backend/pdp2/views.py](https://github.com/projectpai/paipass/blob/main/backend/pdp2/views.py)

and here,

[paipass/backend/pdp2/pdp2.py](https://github.com/projectpai/paipass/blob/main/backend/pdp2/pdp2.py)

and here,

[paipass/core/blockchain/projectpai/pdp/pdp2/pdp2.py](https://github.com/projectpai/paipass/blob/main/core/blockchain/projectpai/pdp/pdp2/pdp2.py)


### Data Flow Diagram


### PDP2 Subscription

The user needs to have an active PDP2 subscription for almost any PDP2 functionality to work. 
 
 
 The source code for the PDP2 Subscription ORM can be found here,
 
 [paipass/pdp2/models.py](https://github.com/projectpai/paipass/blob/main/backend/pdp2/models.py)
 
 This model is called throughout the code found in the pdp2 and yggdrasil directories. Largely it is called to check if the user has a valid PDP2 Subscription but in some cases it is used to store user data.
 
 
  
### Configuration

The configuration defines the behavior that __SubmitUserData__ will exhibit. 


The default configuration largely expects the user's profile to be submitted to the blockchain. 

__SubmitUserData__ will fill in the blanks if there is any prior information found for a correponding dataset to be submitted

### Data Submission


  
