# gvd-exam

## MongoDB: CRUD - Replicacion - Sharding


1. **MongoDB Compass**: Para resolver este ejercicio se utiliza MongoDB Compass con el fin de utilizar el cluster provisto por Mongo Atlas y de esa forma tener disponible *mongosh*, la shell de MongoDB.

2. Se crea la base de datos *mongo_exercise* y la coleccion *movies*.


![compass_data_base](https://github.com/nandroidj/gvd-exam/blob/main/resources/mongo-db-compass.png)

## 1- Documentos a Insertar

  * Insertar los siguientes documentos en una colección llamada movies.

Se procede a dirigirse a la base de datos creada.

````
< use mongo_exercise;
< 'switched to db mongo_exercise'
```

Se insertan las peliculas propuestas en el enunciado.

```
< db.movies.insert([
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

< 'DeprecationWarning: Collection.insert() is deprecated. Use insertOne, insertMany, or bulkWrite.'
< { acknowledged: true,
  insertedIds: 
   { '0': ObjectId("62ca042df1f0162a471ad286"),
     '1': ObjectId("62ca042df1f0162a471ad287"),
     '2': ObjectId("62ca042df1f0162a471ad288"),
     '3': ObjectId("62ca042df1f0162a471ad289"),
     '4': ObjectId("62ca042df1f0162a471ad28a"),
     '5': ObjectId("62ca042df1f0162a471ad28b"),
     '6': ObjectId("62ca042df1f0162a471ad28c"),
     '7': ObjectId("62ca042df1f0162a471ad28d") } }
```



## Punto 2 - Consultas / Buscar documentos

Realizar las siguientes consultas en la coleccion *movies*:

  * Obtener todos los documentos

  ```
    < db.movies.find()
    < { _id: ObjectId("62ca042df1f0162a471ad286"),
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
  ```


  * Obtener documentos con writer igual a "Quentin Tarantino"

  ```
    < db.movies.find({ writer: "Quentin Tarantino"})
    < { _id: ObjectId("62ca042df1f0162a471ad286"),
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
  ```

  * Obtener documentos con actors que incluyan a "Brad Pitt" 4. Obtener documentos con franchise igual a "The Hobbit"

  ```
    < db.movies.find({ actors: { $in: [ "Brad Pitt" ] } })
    < { _id: ObjectId("62ca042df1f0162a471ad286"),
  title: 'Fight Club',
  writer: 'Chuck Palahniuk',
  year: 1999,
  actors: [ 'Brad Pitt', 'Edward Norton' ] }
{ _id: ObjectId("62ca042df1f0162a471ad288"),
  title: 'Inglorious Basterds',
  writer: 'Quentin Tarantino',
  year: 2009,
  actors: [ 'Brad Pitt', 'Diane Kruger', 'Eli Roth' ] }

    < db.movies.find( { franchise: "The Hobbit" } )
    < { _id: ObjectId("62ca042df1f0162a471ad289"),
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
  ```

  * Obtener todas las peliculas de los 90s.

  ```
    < db.movies.find( { year: { $gte: 1990, $lt: 2000 } } )
    < { _id: ObjectId("62ca042df1f0162a471ad286"),
  title: 'Fight Club',
  writer: 'Chuck Palahniuk',
  year: 1999,
  actors: [ 'Brad Pitt', 'Edward Norton' ] }
{ _id: ObjectId("62ca042df1f0162a471ad287"),
  title: 'Pulp Fiction',
  writer: 'Quentin Tarantino',
  year: 1994,
  actors: [ 'John Travolta', 'Uma Thurman' ] }

  ```

  * Obtener las peliculas estrenadas entre el año 2000 y 2010.

  ```
    < db.movies.find( { year: { $gte: 2000, $lt: 2010 } } )
    < { _id: ObjectId("62ca042df1f0162a471ad288"),
  title: 'Inglorious Basterds',
  writer: 'Quentin Tarantino',
  year: 2009,
  actors: [ 'Brad Pitt', 'Diane Kruger', 'Eli Roth' ] }
  ```



## 3- Actualizar Documentos

Agregar sinopsis a "The Hobbit: An Unexpected Journey" : "A reluctant hobbit, Bilbo Baggins, sets out to the Lonely Mountain with a spirited group of dwarves to reclaim their mountain home - and the gold within it - from the dragon Smaug."

Se realiza la busqueda del titulo utilizando el metodo `findOne`

```
  < db.movies.findOne({ title: "The Hobbit: An Unexpected Journey" })
  < { _id: ObjectId("62ca042df1f0162a471ad289"),
  title: 'The Hobbit: An Unexpected Journey',
  writer: 'J.R.R. Tolkein',
  year: 2012,
  franchise: 'The Hobbit' }
```

Luego, se actualiza la pelicula con la funcion `updateOne`

```
  < db.movies.updateOne({ title: "The Hobbit: An Unexpected Journey" }, { $set: {synopsis: "A reluctant hobbit, Bilbo Baggins, sets out to the Lonely Mountain with a spirited group of dwarves to reclaim their mountain home - and the gold within it - from the dragon Smaug."}

  < { acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0 }

```

Finalmente, se chequea que la actualizacion se haya realizado correctamente

```
  < db.movies.findOne({ title: "The Hobbit: An Unexpected Journey" })
  < { _id: ObjectId("62ca042df1f0162a471ad289"),
  title: 'The Hobbit: An Unexpected Journey',
  writer: 'J.R.R. Tolkein',
  year: 2012,
  franchise: 'The Hobbit',
  synopsis: 'A reluctant hobbit, Bilbo Baggins, sets out to the Lonely Mountain with a spirited group of dwarves to reclaim their mountain home - and the gold within it - from the dragon Smaug.' }

```

## 4 - Busqueda por Texto / Text Search

Encontrar las peliculas que en la sinopsis contengan la palabra "Bilbo".

```
  < db.movies.find( { synopsis: { $regex: /Bilbo/ } } )
  < { _id: ObjectId("62ca042df1f0162a471ad289"),
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

```


## 5- Eliminar Documentos

Eliminar la pelicula "Pee Wee Herman's Big Adventure".

```
  < db.movies.remove( { title: "Pee Wee Herman's Big Adventure" } )
  < 'DeprecationWarning: Collection.remove() is deprecated. Use deleteOne, deleteMany, findOneAndDelete, or bulkWrite.'
    { acknowledged: true, deletedCount: 1 }
```



## 6 - Alta Disponibilidad: Replicacion y Sharding



  1. Disenar un cluster con tres nodos (primary,secondary, arbiter) utilizando la colecci�n cargada en el punto anterior.

    ```
      mongod --replSet rs --dbpath /data/db-exam/rs/0 --port 27018 --oplogSize 50
      mongod --replSet rs --dbpath /data/db-exam/rs/1 --port 27019 --oplogSize 50
      mongod --replSet rs --dbpath /data/db-exam/rs/2 --port 27020 --oplogSize 50
    ```

  2.Configurar el cluster con replicacion. Mostrar con printscreens y distintas consultas vistas en clase el correcto funcionamiento del cluster disenado.

    ```
      cfg = {
        _id:"rs",
        members:[
          {_id:0, host:"localhost:27018"},
          {_id:1, host:"localhost:27019"},
          {_id:2, host:"localhost:27020", arbiterOnly:true}
        ]
      };
      rs.initiate(cfg)
    ```

    Luego con `rs.status().members` se obtiene el resultado por el flujo de salida sobre la configuracion propuesta.


  3. Justificar adecuadamente cual podria ser la sharding key correspondiente si nos solicitaran aplicar sharding.

    Considerando que en general se suelen categorizar a las peliculas por titulo, campo `title` del tipo `string`, y MongoDB provee un identificador por cada elemento insertado en una tabla, campo `_id` del tipo `uuid`, se propone que la `sharding key` sea el par (tupla) `[_id, title]` tal que se evite un potencial error en caso de tener dos o mas peliculas con el mismo titulo.

  4. Mostrar el funcionamiento del failover.

    En primer lugar, visualizo el estado del nodo secundario donde se puede ver que los tres servidores se encuentran funcionando correctamente. 

    ```
      rs:SECONDARY> rs.satus().members

      [{
        "version": "1.0",
        "image": {
          "name": "/home/videosdownloader/public_html/image/public/uploadt/Screen Shot 2022-07-09 at 20.56.57.png",
          "baseName": "Screen Shot 2022-07-09 at 20.56.57.png",
          "format": "PNG",
          "formatDescription": "PNG",
          "mimeType": "image/png",
          "class": "DirectClass",
          "geometry": {
            "width": 916,
            "height": 1476,
            "x": 0,
            "y": 0
          },
          "resolution": {
            "x": 144,
            "y": 144
          },
          "printSize": {
            "x": 6.36111,
            "y": 10.25
          },
          "units": "PixelsPerInch",
          "type": "TrueColorAlpha",
          "baseType": "Undefined",
          "endianness": "Undefined",
          "colorspace": "sRGB",
          "depth": 8,
          "baseDepth": 8,
          "channelDepth": {
            "alpha": 1,
            "red": 8,
            "green": 8,
            "blue": 1
          },
          "pixels": 5408064,
          "imageStatistics": {
            "Overall": {
              "min": 13,
              "max": 255,
              "mean": 92.3851,
              "median": 86.75,
              "standardDeviation": 5420.87,
              "kurtosis": -0.915849,
              "skewness": 0.974916,
              "entropy": 0.138457
            }
          },
          "channelStatistics": {
            "alpha": {
              "min": 255,
              "max": 255,
              "mean": 255,
              "median": 255,
              "standardDeviation": 0.000690534,
              "kurtosis": -3,
              "skewness": 3.037e+09,
              "entropy": 4.82164e-05
            },
            "red": {
              "min": 17,
              "max": 249,
              "mean": 50.8747,
              "median": 44,
              "standardDeviation": 6799.31,
              "kurtosis": 17.0354,
              "skewness": 4.09287,
              "entropy": 0.181525
            },
            "green": {
              "min": 13,
              "max": 250,
              "mean": 21.3031,
              "median": 13,
              "standardDeviation": 7762.79,
              "kurtosis": 17.5403,
              "skewness": 4.16518,
              "entropy": 0.18604
            },
            "blue": {
              "min": 17,
              "max": 246,
              "mean": 42.3626,
              "median": 35,
              "standardDeviation": 7121.38,
              "kurtosis": 16.9793,
              "skewness": 4.11195,
              "entropy": 0.186216
            }
          },
          "renderingIntent": "Perceptual",
          "gamma": 0.454545,
          "chromaticity": {
            "redPrimary": {
              "x": 0.64,
              "y": 0.33
            },
            "greenPrimary": {
              "x": 0.3,
              "y": 0.6
            },
            "bluePrimary": {
              "x": 0.15,
              "y": 0.06
            },
            "whitePrimary": {
              "x": 0.3127,
              "y": 0.329
            }
          },
          "matteColor": "#BDBDBD",
          "backgroundColor": "#FFFFFF",
          "borderColor": "#DFDFDF",
          "transparentColor": "#00000000",
          "interlace": "None",
          "intensity": "Undefined",
          "compose": "Over",
          "pageGeometry": {
            "width": 916,
            "height": 1476,
            "x": 0,
            "y": 0
          },
          "dispose": "Undefined",
          "iterations": 0,
          "compression": "Zip",
          "orientation": "Undefined",
          "properties": {
            "date:create": "2022-07-10T00:02:00+00:00",
            "date:modify": "2022-07-10T00:02:00+00:00",
            "exif:ExifOffset": "78",
            "exif:PixelXDimension": "916",
            "exif:PixelYDimension": "1476",
            "exif:UserComment": "65, 83, 67, 73, 73, 0, 0, 0, 83, 99, 114, 101, 101, 110, 115, 104, 111, 116",
            "png:iCCP": "chunk was found",
            "png:IHDR.bit-depth-orig": "8",
            "png:IHDR.bit_depth": "8",
            "png:IHDR.color-type-orig": "6",
            "png:IHDR.color_type": "6 (RGBA)",
            "png:IHDR.interlace_method": "0 (Not interlaced)",
            "png:IHDR.width,height": "916, 1476",
            "png:pHYs": "x_res=5669, y_res=5669, units=1",
            "signature": "664031463af8bcd4723bf70261cbaba4546ca12de6750fecb55657f6a573c43a"
          },
          "profiles": {
            "exif": {
              "length": 144
            },
            "icc": {
              "length": 4088
            }
          },
          "tainted": false,
          "filesize": "579570B",
          "numberPixels": "1.35202M",
          "pixelsPerSecond": "15.8423MB",
          "userTime": "0.110u",
          "elapsedTime": "0:01.085",
          "version": "ImageMagick 7.0.10-58 Q16 x86_64 2021-01-14 https://imagemagick.org"
        }
    }]
    ```

    Acto seguido, se procede a dar de baja el nodo primario, correspondiente al puerto 27018, y en efecto, el nodo secundario pasa a suplantar las tareas que realizaba el primero.

    ```
      rs:PRIMARY> rs.satus().members

      [{
        "version": "1.0",
        "image": {
          "name": "/home/videosdownloader/public_html/image/public/uploadt/Screen Shot 2022-07-09 at 20.56.57.png",
          "baseName": "Screen Shot 2022-07-09 at 20.56.57.png",
          "format": "PNG",
          "formatDescription": "PNG",
          "mimeType": "image/png",
          "class": "DirectClass",
          "geometry": {
            "width": 916,
            "height": 1476,
            "x": 0,
            "y": 0
          },
          "resolution": {
            "x": 144,
            "y": 144
          },
          "printSize": {
            "x": 6.36111,
            "y": 10.25
          },
          "units": "PixelsPerInch",
          "type": "TrueColorAlpha",
          "baseType": "Undefined",
          "endianness": "Undefined",
          "colorspace": "sRGB",
          "depth": 8,
          "baseDepth": 8,
          "channelDepth": {
            "alpha": 1,
            "red": 8,
            "green": 8,
            "blue": 1
          },
          "pixels": 5408064,
          "imageStatistics": {
            "Overall": {
              "min": 13,
              "max": 255,
              "mean": 92.3851,
              "median": 86.75,
              "standardDeviation": 5420.87,
              "kurtosis": -0.915849,
              "skewness": 0.974916,
              "entropy": 0.138457
            }
          },
          "channelStatistics": {
            "alpha": {
              "min": 255,
              "max": 255,
              "mean": 255,
              "median": 255,
              "standardDeviation": 0.000690534,
              "kurtosis": -3,
              "skewness": 3.037e+09,
              "entropy": 4.82164e-05
            },
            "red": {
              "min": 17,
              "max": 249,
              "mean": 50.8747,
              "median": 44,
              "standardDeviation": 6799.31,
              "kurtosis": 17.0354,
              "skewness": 4.09287,
              "entropy": 0.181525
            },
            "green": {
              "min": 13,
              "max": 250,
              "mean": 21.3031,
              "median": 13,
              "standardDeviation": 7762.79,
              "kurtosis": 17.5403,
              "skewness": 4.16518,
              "entropy": 0.18604
            },
            "blue": {
              "min": 17,
              "max": 246,
              "mean": 42.3626,
              "median": 35,
              "standardDeviation": 7121.38,
              "kurtosis": 16.9793,
              "skewness": 4.11195,
              "entropy": 0.186216
            }
          },
          "renderingIntent": "Perceptual",
          "gamma": 0.454545,
          "chromaticity": {
            "redPrimary": {
              "x": 0.64,
              "y": 0.33
            },
            "greenPrimary": {
              "x": 0.3,
              "y": 0.6
            },
            "bluePrimary": {
              "x": 0.15,
              "y": 0.06
            },
            "whitePrimary": {
              "x": 0.3127,
              "y": 0.329
            }
          },
          "matteColor": "#BDBDBD",
          "backgroundColor": "#FFFFFF",
          "borderColor": "#DFDFDF",
          "transparentColor": "#00000000",
          "interlace": "None",
          "intensity": "Undefined",
          "compose": "Over",
          "pageGeometry": {
            "width": 916,
            "height": 1476,
            "x": 0,
            "y": 0
          },
          "dispose": "Undefined",
          "iterations": 0,
          "compression": "Zip",
          "orientation": "Undefined",
          "properties": {
            "date:create": "2022-07-10T00:02:00+00:00",
            "date:modify": "2022-07-10T00:02:00+00:00",
            "exif:ExifOffset": "78",
            "exif:PixelXDimension": "916",
            "exif:PixelYDimension": "1476",
            "exif:UserComment": "65, 83, 67, 73, 73, 0, 0, 0, 83, 99, 114, 101, 101, 110, 115, 104, 111, 116",
            "png:iCCP": "chunk was found",
            "png:IHDR.bit-depth-orig": "8",
            "png:IHDR.bit_depth": "8",
            "png:IHDR.color-type-orig": "6",
            "png:IHDR.color_type": "6 (RGBA)",
            "png:IHDR.interlace_method": "0 (Not interlaced)",
            "png:IHDR.width,height": "916, 1476",
            "png:pHYs": "x_res=5669, y_res=5669, units=1",
            "signature": "664031463af8bcd4723bf70261cbaba4546ca12de6750fecb55657f6a573c43a"
          },
          "profiles": {
            "exif": {
              "length": 144
            },
            "icc": {
              "length": 4088
            }
          },
          "tainted": false,
          "filesize": "579570B",
          "numberPixels": "1.35202M",
          "pixelsPerSecond": "15.8423MB",
          "userTime": "0.110u",
          "elapsedTime": "0:01.085",
          "version": "ImageMagick 7.0.10-58 Q16 x86_64 2021-01-14 https://imagemagick.org"
        }
    }]

    ```

    Por ultimo, se vuelve a dar de alta el servidor caido y se puede observar que persiste como nodo primario el puerto 27019.



  5. Establezca si las siguientes afirmaciones son verdaderas o falsas. Justifique:

    a. Aplicar sharding implica dotar a una infraestructura de HA (High Availability).
  
      **FALSO**: La alta disponibilidad y la redundancia son provistas por la replicacion. Realizar el sharding ofrece tener la informacion distribuida en un cluster.

    b. Una arquitectura que presenta escalamiento vertical permite poder ejecutar procesos Map-Reduce en paralelo.

      **FALSO**: Un escalamiento horizontal es aquel que permite ejectura procesos Map-Reduce en paralelo. 

    c. La presencia de bases NoSQL en una solucion son sinonimo de que estamos ante una problematica de Big Data.

      **FALSO**: No necesariamente la presencia de una base de datos NoSQL porque se trate de resolverlo dentro del ecosistema de Big Data pensando que este tipo de bases también son aplicables en bajos ymedios volumenes de datos. 

    d. La base de config no es requisito mandatorio que cuente con un esquema de HA.

      **VERDADERO**: es necesario en caso de implementar sharding. 

    e. MongoDB soporte tecnicamente un esquema de replicacion Master-Slave.

      **VERDADERO**: es el unico esquema disponible para reaalizar replicacion.



