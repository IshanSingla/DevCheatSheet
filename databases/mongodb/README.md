************************************
# MONGODB BASICS
************************************

### Connect MongoDB Shell
```python
mongo # connects to mongodb://127.0.0.1:27017 by default
mongo --host <host> --port <port> -u <user> -p <pwd> # omit the password if you want a prompt
```
### Show All Databases
```python
show dbs
```

### Show Current Database
```python
db
```


### Create Or Switch Database
```python
use <database_name>
```

### Drop Database
```python
db.dropDatabase()
```


### Create Collection
```python
db.createCollection('posts')
```


### Show Collections
```python
show collections
```


************************************
# CRUD
************************************

### Insert Row
```python
db.posts.insert({
  title: 'Post One',
  body: 'Body of post one',
  category: 'News',
  tags: ['news', 'events'],
  user: {
    name: 'John Doe',
    status: 'author'
  },
  date: Date()
})
```


### Insert Multiple Rows
```python
db.posts.insertMany([
  {
    title: 'Post Two',
    body: 'Body of post two',
    category: 'Technology',
    date: Date()
  },
  {
    title: 'Post Three',
    body: 'Body of post three',
    category: 'News',
    date: Date()
  },
  {
    title: 'Post Four',
    body: 'Body of post three',
    category: 'Entertainment',
    date: Date()
  }
])
```


### Get All Rows
```python
db.posts.find()
```


### Get All Rows Formatted
```python
db.posts.find().pretty()
```


### Find One Row
```python
db.posts.findOne({ category: 'News' })
```


### Find Rows
```python
db.posts.find({ category: 'News' })
```


### Find Specific Fields
```python
db.posts.find({ title: 'Post One' }, {
  title: 1,
  author: 1
})
```


### Update Row
```python
db.posts.update({ title: 'Post Two' },
{
  title: 'Post Two',
  body: 'New body for post 2',
  date: Date()
},
{
  upsert: true
})
```


### Update Specific Field
```python
db.posts.update({ title: 'Post Two' },
{
  $set: {
    body: 'Body for post 2',
    category: 'Technology'
  }
})
```


### Delete Row
```python
db.posts.remove({ title: 'Post Four' })
```


************************************
# OTHER FUNCTIONS
************************************

### Sort Rows
```python
db.posts.find().sort({ title: 1 }).pretty() # asc
db.posts.find().sort({ title: -1 }).pretty() # desc
```


### Count Rows
```python
db.posts.find().count()
db.posts.find({ category: 'news' }).count()
```


### Limit Rows
```python
db.posts.find().limit(2).pretty()
```


### Chaining
```python
db.posts.find().limit(2).sort({ title: 1 }).pretty()
```


### Foreach
```python
db.posts.find().forEach(function(doc) {
  print("Blog Post: " + doc.title)
})
```


### Increment Field (\$inc)
```python
db.posts.update({ title: 'Post Two' },
{
  $inc: {
    likes: 5
  }
})
```


### Rename Field
```python
db.posts.update({ title: 'Post Two' },
{
  $rename: {
    likes: 'views'
  }
})
```


### Sub-Documents
```python
db.posts.update({ title: 'Post One' },
{
  $set: {
    comments: [
      {
        body: 'Comment One',
        user: 'Mary Williams',
        date: Date()
      },
      {
        body: 'Comment Two',
        user: 'Harry White',
        date: Date()
      }
    ]
  }
})
```


### Find By Element in Array (\$elemMatch)
```python
db.posts.find({
  comments: {
     $elemMatch: {
       user: 'Mary Williams'
       }
    }
  }
)
```


### Add Index
```python
db.posts.createIndex({ title: 1 })
```


### Drop Index
```python
db.posts.dropIndex("title_1")
```


### Hide/Unhide Indexes
```python
db.posts.hideIndex("title_1")
db.posts.unhideIndex("title_1")
```


### Text Search
```python
db.posts.find({
  $text: {
    $search: "\"Post O\""
    }
})
```


### Greater & Less Than
```python
db.posts.find({ views: { $gt: 2 } })
db.posts.find({ views: { $gte: 7 } })
db.posts.find({ views: { $lt: 7 } })
db.posts.find({ views: { $lte: 7 } })
```
