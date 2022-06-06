# Comandos del desafio de MongoDB - Coderhouse

*1* - Abrir 2 terminales, en uno de ellos ejecutar:
```
mongod -dbpath ./db
```

show dbs;

use ecommerce;

db.createCollection("mensajes")
db.createCollection("productos")

show collections

db.mensajes.insert([{email: "joseramos@hotmail.com", message: "Hola", date: new Date()},
    {email: "jonathanpardo@gmail.com", message: "¿Como estas?", date: new Date()},
    {email: "joseramos@hotmail.com", message: "Todo bien, ¿vos?", date: new Date()},
    {email: "jonathanpardo@gmail.com", message: "¡Bien! ¿Como va la semana?", date: new Date()},
    {email: "joseramos@hotmail.com", message: "A full con el trabajo, ¿vos?", date: new Date()},
    {email: "jonathanpardo@gmail.com", message: "Igual, jaja, que bueno saber de vos!", date: new Date()},
    {email: "joseramos@hotmail.com", message: "Si! Tenemos que juntarnos mas seguido.", date: new Date()},
    {email: "jonathanpardo@gmail.com", message: "Si. Nos vemos la próxima semana.", date: new Date()},
    {email: "joseramos@hotmail.com", message: "Dale, chau!", date: new Date()},
    {email: "jonathanpardo@gmail.com", message: "Adioss", date: new Date()}])

db.productos.insertMany([{name: "CocaCola 1lt", description: "Lorem ipsum dolor sit amet", stock:123, price:100, thumbnail:"cocacola.com"},
    {name: "Anotador", description: "consectetur adipiscing elit", stock:456, price:120, thumbnail:"anotadores.com"},
    {name: "Calculadora científica", description: "Etiam et gravida sapien", stock:789, price:580, thumbnail:"calculator.com"},
    {name: "Funda para celulares", description: "Praesent vitae ornare risus", stock:101, price:900, thumbnail:"fundas.com"},
    {name: "Reloj", description: "a venenatis felis", stock:121, price:1280, thumbnail:"rolex.com"},
    {name: "Mouse", description: "Morbi id augue ultrices", stock:141, price:1700, thumbnail:"mouse.com"},
    {name: "Bombacha de campo", description: "aliquam velit laoreet", stock:161, price:2300, thumbnail:"latranquera.com"},
    {name: "Webcam", description: "tincidunt purus", stock:181, price:2860, thumbnail:"webcam1080hd.com"},
    {name: "Sartén tramontina", description: "Nullam sit amet lorem imperdiet", stock:202, price:3350, thumbnail:"tramontina.com"},
    {name: "Buzo talle M", description: "pellentesque est et", stock:222 ,price:4786, thumbnail:"nike.com"}])


db.mensajes.find();
db.productos.find();

db.mensajes.estimatedDocumentCount();
db.productos.estimatedDocumentCount();

db.productos.insert({name: "Yerba mate 1kg", description: "gravida lacus", stock:242, price:374, thumbnail:"amanda.com"});

db.productos.find({price: {$lt: 1000}}, {"name": 1});
db.productos.find({price: {$in: [1000, 3000]}}, {"name": 1});
db.productos.find({price: {$gt: 3000}}, {"name": 1});
db.productos.find({}).sort({"price":1}).skip(2).limit(1);

db.productos.updateMany({}, {$set: {"stock": 100}}, {upsert: true});

db.productos.update({price: {$gt: 4000}}, {$set: {"stock": 0}, {multi: true}});

db.productos.remove({price: {$lt: 1000}});

use admin

db.createUser({user: "pepe", pwd: "asd456", roles: [{role: "read", db:"ecommerce"}]})
