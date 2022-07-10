


```
use mongo_exercise;
'switched to db mongo_exercise'

 
use mongo_exercise;
'already on db mongo_exercise'
db.movies.insert([
    {
        "title": "Fight Club",
        "writer": "Chuck Palahniuk",
        "year": 1999,
        "actors": [
            "Brad Pitt",
            "Edward Norton"
        ]
    },
    {
        "title": "Pulp Fiction",
        "writer": "Quentin Tarantino",
        "year" : 1994,
        "actors" : [
            "John Travolta",
            "Uma Thurman"
        ]
    },
    {
        "title" : "Inglorious Basterds",
        "writer" : "Quentin Tarantino",
        "year" : 2009,
        "actors" : [
            "Brad Pitt",
            "Diane Kruger",
            "Eli Roth"
        ]
    },
    {
        "title" : "The Hobbit: An Unexpected Journey",
        "writer" : "J.R.R. Tolkein",
        "year" : 2012,
        "franchise" : "The Hobbit"
    }, 
    {
        "title" : "The Hobbit: The Desolation of Smaug",
        "writer" : "J.R.R. Tolkein",
        "year" : 2013,
        "franchise" : "The Hobbit"
    }, 
    {
        "title" : "The Hobbit: The Battle of the Five Armies",
        "writer" : "J.R.R. Tolkein",
        "year" : 2012,
        "franchise" : "The Hobbit",
    "synopsis" : "Bilbo and Company are forced to engage in a war against an array of combatants and keep the Lonely Mountain from falling into the hands of a rising darkness."
    }, 
    {
        "title" : "Pee Wee Herman's Big Adventure"
    }, 
    {
        "title" : "Avatar"
    }
])
'DeprecationWarning: Collection.insert() is deprecated. Use insertOne, insertMany, or bulkWrite.'
{ acknowledged: true,
  insertedIds: 
   { '0': ObjectId("62ca042df1f0162a471ad286"),
     '1': ObjectId("62ca042df1f0162a471ad287"),
     '2': ObjectId("62ca042df1f0162a471ad288"),
     '3': ObjectId("62ca042df1f0162a471ad289"),
     '4': ObjectId("62ca042df1f0162a471ad28a"),
     '5': ObjectId("62ca042df1f0162a471ad28b"),
     '6': ObjectId("62ca042df1f0162a471ad28c"),
     '7': ObjectId("62ca042df1f0162a471ad28d") } }
db.movies.find()
{ _id: ObjectId("62ca042df1f0162a471ad286"),
  title: 'Fight Club',
  writer: 'Chuck Palahniuk',
  year: 1999,
  actors: [ 'Brad Pitt', 'Edward Norton' ] }
{ _id: ObjectId("62ca042df1f0162a471ad287"),
  title: 'Pulp Fiction',
  writer: 'Quentin Tarantino',
  year: 1994,
  actors: [ 'John Travolta', 'Uma Thurman' ] }
{ _id: ObjectId("62ca042df1f0162a471ad288"),
  title: 'Inglorious Basterds',
  writer: 'Quentin Tarantino',
  year: 2009,
  actors: [ 'Brad Pitt', 'Diane Kruger', 'Eli Roth' ] }
{ _id: ObjectId("62ca042df1f0162a471ad289"),
  title: 'The Hobbit: An Unexpected Journey',
  writer: 'J.R.R. Tolkein',
  year: 2012,
  franchise: 'The Hobbit' }
{ _id: ObjectId("62ca042df1f0162a471ad28a"),
  title: 'The Hobbit: The Desolation of Smaug',
  writer: 'J.R.R. Tolkein',
  year: 2013,
  franchise: 'The Hobbit' }
{ _id: ObjectId("62ca042df1f0162a471ad28b"),
  title: 'The Hobbit: The Battle of the Five Armies',
  writer: 'J.R.R. Tolkein',
  year: 2012,
  franchise: 'The Hobbit',
  synopsis: 'Bilbo and Company are forced to engage in a war against an array of combatants and keep the Lonely Mountain from falling into the hands of a rising darkness.' }
{ _id: ObjectId("62ca042df1f0162a471ad28c"),
  title: 'Pee Wee Herman\'s Big Adventure' }
{ _id: ObjectId("62ca042df1f0162a471ad28d"), title: 'Avatar' }
db.movies.find({ writer: "Quentin Tarantino"})
{ _id: ObjectId("62ca042df1f0162a471ad287"),
  title: 'Pulp Fiction',
  writer: 'Quentin Tarantino',
  year: 1994,
  actors: [ 'John Travolta', 'Uma Thurman' ] }
{ _id: ObjectId("62ca042df1f0162a471ad288"),
  title: 'Inglorious Basterds',
  writer: 'Quentin Tarantino',
  year: 2009,
  actors: [ 'Brad Pitt', 'Diane Kruger', 'Eli Roth' ] }
db.movies.find({ actors: { $in: [ "Brad Pitt" ] } })
{ _id: ObjectId("62ca042df1f0162a471ad286"),
  title: 'Fight Club',
  writer: 'Chuck Palahniuk',
  year: 1999,
  actors: [ 'Brad Pitt', 'Edward Norton' ] }
{ _id: ObjectId("62ca042df1f0162a471ad288"),
  title: 'Inglorious Basterds',
  writer: 'Quentin Tarantino',
  year: 2009,
  actors: [ 'Brad Pitt', 'Diane Kruger', 'Eli Roth' ] }
db.movies.find( { franchise: "The Hobbit" } )
{ _id: ObjectId("62ca042df1f0162a471ad289"),
  title: 'The Hobbit: An Unexpected Journey',
  writer: 'J.R.R. Tolkein',
  year: 2012,
  franchise: 'The Hobbit' }
{ _id: ObjectId("62ca042df1f0162a471ad28a"),
  title: 'The Hobbit: The Desolation of Smaug',
  writer: 'J.R.R. Tolkein',
  year: 2013,
  franchise: 'The Hobbit' }
{ _id: ObjectId("62ca042df1f0162a471ad28b"),
  title: 'The Hobbit: The Battle of the Five Armies',
  writer: 'J.R.R. Tolkein',
  year: 2012,
  franchise: 'The Hobbit',
  synopsis: 'Bilbo and Company are forced to engage in a war against an array of combatants and keep the Lonely Mountain from falling into the hands of a rising darkness.' }
db.movies.find( { year: { $gte: 1990, $lt: 2000 } } )
{ _id: ObjectId("62ca042df1f0162a471ad286"),
  title: 'Fight Club',
  writer: 'Chuck Palahniuk',
  year: 1999,
  actors: [ 'Brad Pitt', 'Edward Norton' ] }
{ _id: ObjectId("62ca042df1f0162a471ad287"),
  title: 'Pulp Fiction',
  writer: 'Quentin Tarantino',
  year: 1994,
  actors: [ 'John Travolta', 'Uma Thurman' ] }
db.movies.find( { year: { $gte: 2000, $lt: 2010 } } )
{ _id: ObjectId("62ca042df1f0162a471ad288"),
  title: 'Inglorious Basterds',
  writer: 'Quentin Tarantino',
  year: 2009,
  actors: [ 'Brad Pitt', 'Diane Kruger', 'Eli Roth' ] }
db.movies.findOne({ title: "The Hobbit: An Unexpected Journey" })
{ _id: ObjectId("62ca042df1f0162a471ad289"),
  title: 'The Hobbit: An Unexpected Journey',
  writer: 'J.R.R. Tolkein',
  year: 2012,
  franchise: 'The Hobbit' }
db.movies.updateOne({ title: "The Hobbit: An Unexpected Journey" }, { $set: {synopsis: "A reluctant hobbit, Bilbo Baggins, sets out to the Lonely Mountain with a spirited group of dwarves to reclaim their mountain home - and the gold within it - from the dragon Smaug."} })
{ acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0 }
db.movies.findOne({ title: "The Hobbit: An Unexpected Journey" })
{ _id: ObjectId("62ca042df1f0162a471ad289"),
  title: 'The Hobbit: An Unexpected Journey',
  writer: 'J.R.R. Tolkein',
  year: 2012,
  franchise: 'The Hobbit',
  synopsis: 'A reluctant hobbit, Bilbo Baggins, sets out to the Lonely Mountain with a spirited group of dwarves to reclaim their mountain home - and the gold within it - from the dragon Smaug.' }
db.movies.find( { synopsis: { $regex: /Bilbo/ } } )
{ _id: ObjectId("62ca042df1f0162a471ad289"),
  title: 'The Hobbit: An Unexpected Journey',
  writer: 'J.R.R. Tolkein',
  year: 2012,
  franchise: 'The Hobbit',
  synopsis: 'A reluctant hobbit, Bilbo Baggins, sets out to the Lonely Mountain with a spirited group of dwarves to reclaim their mountain home - and the gold within it - from the dragon Smaug.' }
{ _id: ObjectId("62ca042df1f0162a471ad28b"),
  title: 'The Hobbit: The Battle of the Five Armies',
  writer: 'J.R.R. Tolkein',
  year: 2012,
  franchise: 'The Hobbit',
  synopsis: 'Bilbo and Company are forced to engage in a war against an array of combatants and keep the Lonely Mountain from falling into the hands of a rising darkness.' }
db.movies.remove( { title: "Pee Wee Herman's Big Adventure" } )
'DeprecationWarning: Collection.remove() is deprecated. Use deleteOne, deleteMany, findOneAndDelete, or bulkWrite.'
{ acknowledged: true, deletedCount: 1 }
```
