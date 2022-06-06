# Comandos del desafio de MongoDB - Coderhouse

**1** - Abrir 2 terminales, en uno de ellos ejecutar:
```
mongod -dbpath ./db
```  
**2** - Seguido a esto efectuar éste otro comando, para conseguir la conexión con la base de datos:
```
mongo
```  
## Una vez realizado el paso anterior, vamos a crear lo solicitado por la actividad en la database

### **1** - Para verificar que la conexión fue correcta, usar esto para ver que bases de datos tenemos creadas:
```
show dbs
```  
**2** - Para utilizar y/o crear la base, vamos a ejecutar:
```
use ecommerce
```  
**3** - A continuación, crearemos las colecciones de mensajes y de productos con: 
```
db.createCollection("mensajes")
```  
Y  
```
db.createCollection("productos")
```  
**4** - Corroboraremos que ambas se crearon con:
```
show collections
```  
## Ahora sí, vamos a insertar datos en las coleciones
**1** - Para insertar los 10 mensajes que solicitaron en la actividad, ejecutar:
``` 
db.mensajes.insertMany([{email: "joseramos@hotmail.com", message: "Hola", date: new Date()},
    {email: "jonathanpardo@gmail.com", message: "¿Como estas?", date: new Date()},
    {email: "joseramos@hotmail.com", message: "Todo bien, ¿vos?", date: new Date()},
    {email: "jonathanpardo@gmail.com", message: "¡Bien! ¿Como va la semana?", date: new Date()},
    {email: "joseramos@hotmail.com", message: "A full con el trabajo, ¿vos?", date: new Date()},
    {email: "jonathanpardo@gmail.com", message: "Igual, jaja, que bueno saber de vos!", date: new Date()},
    {email: "joseramos@hotmail.com", message: "Si! Tenemos que juntarnos mas seguido.", date: new Date()},
    {email: "jonathanpardo@gmail.com", message: "Si. Nos vemos la próxima semana.", date: new Date()},
    {email: "joseramos@hotmail.com", message: "Dale, chau!", date: new Date()},
    {email: "jonathanpardo@gmail.com", message: "Adioss", date: new Date()}])
```  
**2** - Para insertar los 10 productos que solicitan, efectuar:
``` 
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
```   
**3** - Para listar todos los documentos de las colecciones usar:
``` 
db.mensajes.find()
```   
``` 
db.productos.find()
```   
**4** - Ejecutar el siguiente comando para mostrar la cantidad de documentos en cada colección
``` 
db.mensajes.estimatedDocumentCount()
```   
``` 
db.productos.estimatedDocumentCount()
```   
**5** - Luego insertaremos un nuevo producto con:
``` 
db.productos.insert({name: "Yerba mate 1kg", description: "gravida lacus", stock:242, price:374, thumbnail:"amanda.com"})
```  
**6** - Listaremos los productos menores a $1000, usando:
``` 
db.productos.find({price: {$lt: 1000}}, {"name": 1})
```   
Tras eso filtraremos los productos que se encuentran entre $1000 y $3000
``` 
db.productos.find({price: {$in: [1000, 3000]}}, {"name": 1})
``` 
Despues los mayores a $3000:
``` 
db.productos.find({price: {$gt: 3000}}, {"name": 1})
``` 
Seguidamente traeremos el 3er producto mas barato:
``` 
db.productos.find({}).sort({"price":1}).skip(2).limit(1)
``` 
**7** - Posteriormente actualizaremos el stock a 100 a todos los productos:
``` 
db.productos.updateMany({}, {$set: {"stock": 100}}, {upsert: true})
``` 
A continuacion, vamos a cambiar el stock a 0 a aquellos productos que valen mas de $4000:
``` 
db.productos.update({price: {$gt: 4000}}, {$set: {"stock": 0}, {multi: true}});
``` 
Posterior a esto, borraremos todos los productos mentores a $1000,usando:
db.productos.remove({price: {$lt: 1000}});

**8** Ahora crearemos un usuario con unicamente permisos de lectura:  
usaremos 
use admin

db.createUser({user: "pepe", pwd: "asd456", roles: [{role: "read", db:"ecommerce"}]})
