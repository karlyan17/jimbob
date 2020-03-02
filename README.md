# JIMbob 
JSON In Memory ... bob
is a minimal "document database" suitable for small projects, where all the data can easily be stored in memory.
The advantage over other similar implementations is, that everything is saved as JSON files in an easy to navigate directory structure

## Struct

### Bucket
```
type Bucket struct {
    Path string
    Data map[int]interface{}
    next_index int
}
```

Primary and only datastructure. It implements implements a simple CrUD interface (the r is lowercase, because accessing the data is not done by a function but directly as the value of the struct, implementation of such a function is left to the user as a simplke exercise ;) ) 

## Functions

### OpenBucket()
```
OpenBucket(string) (Bucket,error)
```

opens an existing jimbob bucket stored at the given path.

#### Usage
```
db,err = jimbob.OpenBucket("path/to/db")
```

### Bucket.Post()
```
(*Bucket) Post(interface{}) (int, error)
```

POST (write) given data into the jimbob bucket and returns the data's index

#### Usage
```
index,err = db.Post(some_data)
```

### Bucket.Delete()
```
(*Bucket) Delete(int) error
```

Delete data entry with the given index.

#### Usage
```
err = db.Delete(420)
```

#### WriteOut()
```
WriteOut(string,map[int]interface{}) error
```

Writes some given data to a specified path, essentially creating a new jimbob bucket.
This function is used both internally to commit changes and can be used to create a new jimbob bucket out of any data in the form `map[int]interface()`

##### Usage
```
// write data to disk
err = WriteOut(path_to_bucket, customers_map)

// read the exported data as a jimbob bucket
db,err = OpenBucket(path_to_bucket)
