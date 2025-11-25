# mongo_vinos
Este repositorio contiene la base de datos creada en MongoDB para el análisis del dataset winequality-red.csv. 
Se incluyen las consultas básicas, consultas avanzadas y operaciones CRUD realizadas durante la fase del proyecto.
1. Inserción de documentos
   db.Vinos.insertOne({
  "fixed acidity": 8.0,
  "volatile acidity": 0.5,
  "citric acid": 0.3,
  "residual sugar": 2.5,
  "chlorides": 0.08,
  "free sulfur dioxide": 15,
  "total sulfur dioxide": 40,
  "density": 0.9968,
  "pH": 3.4,
  "sulphates": 0.65,
  "alcohol": 10.0,
  "quality": 6
})
3. Consultas básicas (find)
   db.Vinos.find().limit(5)
   filtar vinos de calidad ≥ 7:
db.Vinos.find({ quality: { $gte: 7 } })

3. Actualización de documentos
   db.Vinos.updateOne({ quality: 5 }, { $set: { quality: 6 } })
   
5. Eliminación de documentos
   db.Vinos.deleteOne({ alcohol: { $lt: 8 } })
   
6. Filtros con operadores
   db.Vinos.find({ pH: { $gte: 3.2, $lte: 3.5 }})
db.Vinos.find({
  $and: [{ alcohol: { $gt: 12 } },
{ quality: { $gt: 6 } }]})

7. Consultas de agregación
db.Vinos.aggregate

Conteo por nivel de calidad:
([{ $group: { _id: "$quality", total: { $sum: 1 } } }, { $sort: { _id: 1 } }])

Promedio general del pH:
db.Vinos.aggregate([{ $group: { _id: null, promedioPH: { $avg: "$pH" } } }])

Promedio de alcohol por calidad:
db.Vinos.aggregate([{ $group: { _id: "$quality", promedioAlcohol: { $avg: "$alcohol" } } },{ $sort: { _id: 1 } }])


