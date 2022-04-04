# MongoDB
Basic MongoDB Commands

![mongoDB](https://www.cloudsavvyit.com/p/uploads/2021/07/f5932bc2.jpg?width=1198&trim=1,1&bg-color=000&pad=1,1)

Show all Databases
---
> show dbs

Show current Database
---
> db

Create or Switch Database
---
> use db_name

Drop Database
---
> db.dropDatabase()

Create Collection (as Create Table)
---
> db.createCollection('posts')

Show Collections
---
> show Collections

Insert Row
---
> db.posts.insert({
  title : 'Post One',
  body : 'Body of post one',
  category : 'News',
  tags : ['news','events']
  user : {
  name : 'Ayoub Kassi',
  status : 'author'
},
  date : Date()
})

Insert Multiple Rows
---
> db.posts.insertMany([
{
  title : 'Post two',
  body : 'Body of post two',
  category : 'Technology',
  date : Date()
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

Get All Row
---
> db.posts.find()

Get All Rows Formatted
---
> db.posts.find().pretty()

Find Rows
---
> db.posts.find({category : 'News'})

Sort Rows
---
> # asc
> db.posts.find().sort({title : 1}).pretty()
> # desc
> db.posts.find().sort({title : -1}).pretty()

Count Rows
---
> db.posts.find().count()

Chaining
---
> db.posts.find().limit(2).sort({title : 1}).pretty()

Foreach
---
> db.posts.find().forEach(function(doc){
  print("Blog Post : "+ doc.title)
})

Find One Row
---
> db.posts.findOne({category : 'News'})

Find Specific Fields
---
> db.posts.find({ title : 'Post One'}, {
  title : 1,
  author : 1
})

Update Specific Field
---
> db .posts.update({title : 'Post Two'}, {
  $set : {
  body : 'Body for post 2',
  category : 'Technology'
}
})

Increment Field
---
> db.posts.update({ title : 'Post Two'},
{
  $inc : {
    likes : 5
}
})

Rename Filed
---
> db.posts.update({title : 'Post Two'},{
  $rename : {
  likes : 'views'
}
})

Delete Row
---
> db.posts.remove({title : 'Post Four'})

Sub-Documents
---
> db.posts.update({ title: 'Post One' },
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

Find By Element in Array($elementMatch)
---
> db.posts.find({
  comments: {
     $elemMatch: {
       user: 'Mary Williams'
       }
    }
  }
)

Add Index
---
> db.posts.createIndex({ title : 'text'})

Text Search
---
> db.posts.find({
  $text: {
    $search: "\"Post O\""
    }
})

Greater & less than
---
> db.posts.find({ views: { $gt: 2 } })
db.posts.find({ views: { $gte: 7 } })
db.posts.find({ views: { $lt: 7 } })
db.posts.find({ views: { $lte: 7 } })
