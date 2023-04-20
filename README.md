# Table of contents
- [Table of contents](#table-of-contents)
- [Backend con Node JS: API REST con Express.js](#backend-con-node-js-api-rest-con-expressjs)

# Backend con Node JS: API REST con Express.js
¡Aprende desarrollo backend con Node.js! Trabaja con rutas, servidores y middlewares de Express.js. Construye una API, manipula errores y haz validación de datos. Despliega tu aplicación a producción en Heroku. Conviértete en backend developer con Node.js.

- Usa Node.js con Express.js para el backend de tu aplicación
- Crea los endpoints de tu API REST
- Crea tu primer servidor HTTP

## Introduccion
### ¿Que es Express.js?
Express es un framework de Node.js utilizado para construir aplicaciones web del lado del servidor. Es rápido, minimalista y cuenta con un conjunto de características robustas y de alto rendimiento para aplicaciones web y móviles. Express proporciona una capa de abstracción sobre la API HTTP en Node.js, lo que facilita la creación de aplicaciones y servicios web altamente escalables y mantenibles.

### Configuracion del entorno de desarrollo para este curso
1. [Clase](https://platzi.com/clases/2485-backend-nodejs/41744-configuracion-del-entorno-de-desarrollo/)

*Nota*
ESLint es una herramienta de linting de JavaScript que identifica y reporta patrones en el código JavaScript. Un linter es una herramienta que analiza el código fuente para señalar errores de sintaxis, detectar posibles problemas, y aplicar ciertas reglas de programación para mejorar la calidad del código, aumentar la eficiencia en la escritura y el mantenimiento del código, y evitar posibles errores de programación. En términos sencillos, un linter funciona como un corrector ortográfico para el código, identificando errores de escritura y sugiriendo cómo corregirlos.

### Instalacion de Express.js y tu primer servidor HTTP
1. [Clase](https://platzi.com/clases/2485-backend-nodejs/41744-configuracion-del-entorno-de-desarrollo/)

#### Codigo
```javascript
const express = require('express');
const app = express();
const port = 3000;

app.get('/',(req,res) =>{
  res.send('Hello World');
});

app.listen(port, () => {
  console.log('Mi port' + port);
});
```
2. [Documentacion de Express JS](https://expressjs.com/)

### Routing con Express.js
1. [Clase](https://platzi.com/clases/2485-backend-nodejs/41745-instalacion-de-expressjs-y-tu-primer-servidor-http/)


```javascript
app.get('/nueva-ruta',(req,res) =>{
  res.send('Hola, soy una nueva ruta');
});

app.get('/productos',(req,res) =>{
  res.json({
    name: 'Producto 1',
    price: 1000
  });
});

```

## CRUD
### ¿Que es una RESTful API?
Un RESTful API (Application Programming Interface) es un modelo de arquitectura para sistemas de comunicación entre diferentes aplicaciones. Este tipo de API utiliza el protocolo HTTP para realizar operaciones con los recursos disponibles en un servidor. Una API RESTful está formada por recursos, que son objetos o datos que se almacenan en el servidor y se pueden consultar, crear, modificar o borrar. Cada recurso tiene una URL única que permite acceder a él mediante los métodos de HTTP correspondientes (GET, POST, PUT, DELETE, etc.). También se utiliza el formato JSON para el intercambio de datos entre el servidor y la aplicación que consume la API.

GET, PUT, DELETE, y POST son los principales métodos utilizados en una API RESTful para realizar operaciones en los recursos disponibles en un servidor. Aquí te explico brevemente para qué sirve cada uno:

- GET: Es utilizado para solicitar una representación del recurso especificado en la URL. Normalmente se utiliza para leer información.

- POST: Sirve para crear un nuevo recurso en el servidor. Por ejemplo, se puede utilizar para enviar información de un formulario a un servidor que luego crea un nuevo objeto.

- PUT: Se utiliza para actualizar un recurso existente en el servidor. Por ejemplo, si un usuario quiere cambiar algún dato de un perfil, se puede realizar una solicitud PUT para actualizar la información.
  
- DELETE: Sirve para eliminar un recurso existente en el servidor. Por ejemplo, si un usuario quiere eliminar su perfil, se puede utilizar una solicitud DELETE para que el servidor elimine los datos correspondientes.
  
Es importante mencionar que estos métodos no son los únicos que se pueden utilizar en una API RESTful, pero son los más comunes y recomendados por convención.

![Image](https://static.platzi.com/media/user_upload/REST-65e4240f-662b-406e-91c9-57d8b0dd56f4.jpg)

1. [Clase](https://platzi.com/clases/2485-backend-nodejs/41747-que-es-una-restful-api/)

### GET: recibir parametros
```javascript
app.get('/products',(req,res) =>{
  res.json([
    {
      name: 'Producto 1',
      price: 1000
    },
    {
      name: 'Producto 2',
      price: 2000
    }
  ]);
});

app.get('/products/:id',(req,res) =>{
  const { id } = req.params;
  res.json({
    id,
    name: 'Producto 1',
    price: 1000
  });
});

app.get('/categories/:category_id/products/:product_id',(req,res) =>{
  const { category_id, product_id } = req.params;
  res.json({
    category_id,
    product_id
  });
})
```
### GET: parámetros query
Los query parameters, también conocidos como parámetros de consulta, son una forma de agregar información adicional a una solicitud GET. Estos parámetros se agregan a la URL de la solicitud después del signo de interrogación (?), y consisten en una clave y un valor separados por el signo igual (=), por ejemplo: 

https://api.example.com/customers?sortBy=name&limit=10.

Los query parameters permiten a los clientes de la API RESTful solicitar datos más específicos y detallados del recurso que se está solicitando. Por ejemplo, un cliente puede utilizar los parámetros de consulta para ordenar los resultados de una búsqueda, filtrar información o paginar los resultados. En general, los parámetros de consulta son una buena forma de optimizar la experiencia del usuario final, proporcionándole solo la información que necesita y reduciendo el tiempo de procesamiento del servidor.

Hay varios query parameters comúnmente utilizados en las solicitudes GET de una API RESTful. Algunos de los más populares son:

- **sort**: ordena los resultados de la búsqueda por un campo determinado (por ejemplo, sort=name ordena los resultados por el nombre)

- **filter**: filtra los resultados por un criterio específico (por ejemplo, filter=category:books muestra solo los resultados de la categoría de libros)

- **page**: permite la paginación de los resultados para mostrar una cantidad específica de resultados en una página (por ejemplo, page=2&limit=10 muestra los resultados de la página 2 con un límite de 10 resultados por página)

- **limit**: limita la cantidad de resultados que se muestran en una sola solicitud (por ejemplo, limit=25 muestra solo los primeros 25 resultados)

- **fields**: muestra solo los campos específicos de un recurso determinado (por ejemplo, fields=name,age muestra solo los campos de nombre y edad)

En general, estos parámetros de consulta son útiles para personalizar las solicitudes GET y obtener información más específica y útil de la API RESTful.

```javascript
app.get('/products',(req,res) =>{
  const products = [];
  const {size} = req.query;
  const limit = size || 10;
  for (let i = 0; i < limit; i++) {
    products.push({
      name: faker.commerce.productName(),
      price: parseInt(faker.commerce.price(),10),
      image: faker.image.imageUrl()
    });
  }
  res.json(products);
});
```
**Nota**
Cuando tengo ENDPoints similares como estos

```javascript
app.get('/products/filter',(req,res) =>{
  res.send('Filtrando productos');
});

app.get('/products/:id',(req,res) =>{
  const { id } = req.params;
  res.json({
    id,
    name: 'Producto 1',
    price: 1000
  });
});
```
debe ir primero los fijos y luego los dinamicos 

1. [Clase](https://platzi.com/clases/2485-backend-nodejs/41748-get-parametros-query/)

### Separacion de responsabilidades con express.Router

El principio de responsabilidad única (Single Responsibility Principle) es un principio dentro del desarrollo de software que establece que una clase o módulo debe tener solo una responsabilidad o motivo para cambiar. Esto significa que una clase debe tener una y solo una razón para cambiar, lo que la hace más fácil de mantener y entender. Si una clase asume varias responsabilidades, puede volverse difícil de mantener a medida que evoluciona el software y puede ser difícil de reutilizar. 

En resumen, el principio de responsabilidad única se enfoca en que un componente de software debe tener un solo propósito o función de manera que pueda ser fácilmente entendido, modificado y mantenido sin afectar otros componentes.

1. Se crea una carperta Router: alli iran las diferentes rutas
  ```javascript
  const express = require('express');
  const {faker} = require('@faker-js/faker');

  const router = express.Router();

  router.get('/',(req,res) =>{
    const products = [];
    const {size} = req.query;
    const limit = size || 10;
    for (let i = 0; i < limit; i++) {
      products.push({
        name: faker.commerce.productName(),
        price: parseInt(faker.commerce.price(),10),
        image: faker.image.imageUrl()
      });
    }
    res.json(products);
  });

  router.get('/filter',(req,res) =>{
    res.send('Filtrando productos');
  });

  router.get('/:id',(req,res) =>{
    const { id } = req.params;
    res.json({
      id,
      name: 'Producto 1',
      price: 1000
    });
  });

  module.exports = router;
   ```
  
2. Se crea el archivo index de las rutas
```javascript
const productsRouter = require('./productsRouter');
// const usersRouter = require('./usersRouter');

function routerApi(app) {
  app.use('/products', productsRouter)
  // app.use('/users', usersRouter')
}

module.exports = routerApi;
```
3. Se actualiza el index
```javascript 
const express = require('express');
const routerApi = require('./routes');

const app = express();
const port = 3000;

routerApi(app);

app.listen(port, () => {
  console.log('Mi port' + port);
});
```

### Instalacion de Postman o Insomia
En este caso, yo utilizo ThunderClient la cual es una extesion de VSCode. Para instalar Postman o Insomia, visita el siguiente enlace

[Instalacion Postman e Insomia](https://platzi.com/clases/2485-backend-nodejs/41750-instalacion-de-postman-o-insomia/)

### POST: metodo para crear
#### Buenas practicas para rutas
```javascript
const express = require('express');

const productsRouter = require('./products.router');
const categoriesRouter = require('./categories.router');
const usersRouter = require('./users.router');

function routerApi(app) {
  const router = express.Router();
  app.use('/api/v1', router);
  router.use('/products', productsRouter);
  router.use('/categories', categoriesRouter);
  router.use('/users', usersRouter);
}

module.exports = routerApi;
```
1. Crear un metodo POST
```javascript
router.post('/',(req,res) =>{
  const body = req.body;
  res.json({
    message: 'created',
    data: body
  });
});
```
2. Actualizar index.js para que permita verificar los JSON

```javascript
const app = express();
const port = 3000;

app.use(express.json());
```
3. [Clase](https://platzi.com/clases/2485-backend-nodejs/41751-post-metodo-para-crear/)

### PUT, PATCH y DELETE
```javascript
router.post('/',(req,res) =>{
  const body = req.body;
  res.json({
    message: 'created',
    data: body
  });
});

router.patch('/:id',(req,res) =>{
  const { id } = req.params;
  const body = req.body;
  res.json({
    message: 'update',
    data: body,
    id
  });
});

router.delete('/:id',(req,res) =>{
  const { id } = req.params;
  res.json({
    message: 'deleted',
    id
  });
});
```
1. [Clase](https://platzi.com/clases/2485-backend-nodejs/41752-put-patch-y-delete/)

### Codigos de estado o HTTP response status codes
Los status code o códigos de estado son números de tres dígitos que se utilizan en las respuestas de las solicitudes HTTP y que indican el resultado de dicha operación. Estos códigos se dividen en cinco clases principales, y cada una de ellas tiene un rango de valores asociado:

- Clase 1xx: indica una respuesta informativa.
- Clase 2xx: indica una respuesta satisfactoria.
- Clase 3xx: indica una redirección.
- Clase 4xx: indica un error del cliente.
- Clase 5xx: indica un error del servidor.

Algunos ejemplos comunes de códigos de estado son:

- 200 OK: indica que la solicitud se ha procesado correctamente.
- 400 Bad Request: indica que la solicitud es inválida o está mal formada.
- 401 Unauthorized: indica que el usuario no está autorizado para acceder al recurso solicitado.
- 404 Not Found: indica que el recurso solicitado no se ha encontrado en el servidor.
- 500 Internal Server Error: indica un error interno del servidor.

Los códigos de estado son útiles para la depuración y el monitoreo de una API, ya que permiten identificar rápidamente qué ha pasado en cada solicitud y cómo se ha comportado el servidor.

2. [Http Cats](https://http.cat/)

```javascript
router.get('/:id',(req,res) =>{
  const { id } = req.params;
  if (id === '999') {
    res.status(404).json({
      message: 'Product not found'
    });
  } else {
    res.json({
      id,
      name: 'Producto 1',
      price: 1000
    });
  }
});

router.post('/',(req,res) =>{
  const body = req.body;
  res.status(201).json({
    message: 'created',
    data: body
  });
});

```

## Servicios 
### Introduccion a servicios: crea tu primer servicio
1. [Clase](https://platzi.com/clases/2485-backend-nodejs/41754-introduccion-a-servicios-crea-tu-primer-servicio/)

1. Crear carpeta services
2. Crear archivo product.service.js
```javascript
const {faker} = require('@faker-js/faker');

class ProductServices {

    constructor(){
        this.products = [];
        this.generate();

    }

    generate(){
        const limit = 100;
        for (let i = 0; i < limit; i++) {
          this.products.push({
            id: faker.datatype.uuid(),
            name: faker.commerce.productName(),
            price: parseInt(faker.commerce.price(),10),
            image: faker.image.imageUrl()
          });
        }
    }

    create(){

    }

    find(){
        return this.products;
    }

    findOne(id){
        return this.products.find(item => item.id === id);
    }

    update(){

    }
    
    delete(){

    }
}

module.exports = ProductServices;
```
3. Actualizar el archivo products.router.js
```javascript
const express = require('express');

const ProductServices = require('../services/product.service');

const router = express.Router();
const service =  new ProductServices();

router.get('/',(req,res) =>{
  const products = service.find();
  res.json(products);
});

router.get('/filter',(req,res) =>{
  res.send('Filtrando productos');
});

router.get('/:id',(req,res) =>{
  const { id } = req.params;
  const product = service.findOne(id);
  res.json(product);
});

...
```

### Crear, editar y eliminar
[Clase](https://platzi.com/clases/2485-backend-nodejs/41755-crear-editar-y-eliminar/)

1. Actualizar el archivo product.service.js
```javascript

    update(id, changes){
        const index = this.products.findIndex(item => item.id === id);
        if (index === -1) {
            throw new Error('Product not found');
        }
        const product = this.products[index];
        this.products[index] = {
            ...product,
            ...changes
        };
        return this.products[index];
    }
    
    delete(id){
        const index = this.products.findIndex(item => item.id === id);
        if (index === -1) {
            throw new Error('Product not found');
        }
        this.products.splice(index,1);
        return {id}; 
    }

```

2. Actualizar el archivo products.router.js
```javascript
router.post('/',(req,res) =>{
  const body = req.body;
  const newProduct = service.create(body);
  res.status(201).json(newProduct);
});

router.patch('/:id',(req,res) =>{
  const { id } = req.params;
  const body = req.body;
  const product = service.update(id,body);
  res.json(product);
});

router.delete('/:id',(req,res) =>{
  const { id } = req.params;
  const rta = service.delete(id);
  res.json(rta);
});
```

### Async, await y captura de errores
[Clase](https://platzi.com/clases/2485-backend-nodejs/41756-async-await-y-captura-de-errores/)

1. Actualizar product services (Async y await)
```javascript
const {faker} = require('@faker-js/faker');

class ProductServices {

    constructor(){
        this.products = [];
        this.generate();

    }

    generate(){
        const limit = 100;
        for (let i = 0; i < limit; i++) {
          this.products.push({
            id: faker.datatype.uuid(),
            name: faker.commerce.productName(),
            price: parseInt(faker.commerce.price(),10),
            image: faker.image.imageUrl()
          });
        }
    }

    async create(data){
        const newProduct = {
            id: faker.datatype.uuid(),
            ...data
        }
        this.products.push(newProduct);
        return newProduct;
    }

    async find(){
        return new Promise((resolve,reject) =>{
            setTimeout(() =>{
                resolve(this.products);
                }, 5000);
        });
    }

    async findOne(id){
        return this.products.find(item => item.id === id);
    }

    async update(id, changes){
        const index = this.products.findIndex(item => item.id === id);
        if (index === -1) {
            throw new Error('Product not found');
        }
        const product = this.products[index];
        this.products[index] = {
            ...product,
            ...changes
        };
        return this.products[index];
    }
    
    async delete(id){
        const index = this.products.findIndex(item => item.id === id);
        if (index === -1) {
            throw new Error('Product not found');
        }
        this.products.splice(index,1);
        return {id}; 
    }
}
...
```
2. Actualizar products.router.js (Async y await)
```javascript
const express = require('express');

const ProductServices = require('../services/product.service');

const router = express.Router();
const service =  new ProductServices();

router.get('/', async (req,res) =>{
  const products = await service.find();
  res.json(products);
});

router.get('/:id', async (req,res) =>{
  const { id } = req.params;
  const product = await service.findOne(id);
  res.json(product);
});

router.post('/',async (req,res) =>{
  const body = req.body;
  const newProduct = await service.create(body);
  res.status(201).json(newProduct);
});

router.patch('/:id',async (req,res) =>{
  try {
    const { id } = req.params;
    const body = req.body;
    const product = await service.update(id,body);
    res.json(product);
  } catch (error) {
    res.status(404).json({
      message: error.message
    });
  }
});

router.delete('/:id',async (req,res) =>{
  const { id } = req.params;
  const rta = await service.delete(id);
  res.json(rta);
});
...
```

## Middlewares
### Que son los middlewares
En el contexto de la programación de software, un middleware es un software que actúa como intermediario entre diferentes aplicaciones o componentes de una misma aplicación. Los middlewares se utilizan para facilitar la comunicación y el intercambio de información entre diferentes sistemas, ya que proporcionan una capa de abstracción que oculta las complejidades de los sistemas subyacentes.

Los middlewares pueden tener diversas funcionalidades, como por ejemplo:

- Transformar los datos de un formato a otro para que puedan ser procesados por diferentes sistemas.
- Proporcionar una capa de seguridad adicional para proteger los datos en tránsito entre diferentes sistemas.
- Controlar y gestionar el flujo de información entre diferentes sistemas para evitar congestiones o cuellos de botella.
- Realizar tareas de autenticación y autorización para garantizar que solo los usuarios autorizados puedan acceder a los datos o servicios ofrecidos por una aplicación.

En resumen, los middlewares son una herramienta muy útil para facilitar la integración y la interoperabilidad entre diferentes sistemas y aplicaciones en el desarrollo de software.

[Clase](https://platzi.com/clases/2485-backend-nodejs/41757-que-son-los-middlewares/)

### Middleware para HttpErrors
[Clase](https://platzi.com/clases/2485-backend-nodejs/41758-middleware-para-httperrors/)

1. Crear carpeta middlewares
2. crear archivo error.handler.js
```javascript
function logErrors(err, req, res, next){
    console.error(err);
    next(err)
}

function errorHandler(err, req, res, next){
    res.status(500).json({
        message: err.message,
        stack: err.stack
    });
}

module.exports = {logErrors};
```
3. Actualizar index.js
```javascript
const express = require('express');
const routerApi = require('./routes');

const {logErrors, errorHandler} = require('./middlewares/error.handler');

const app = express();
const port = 3000;

app.use(express.json());

app.get('/',(req,res) =>{
  res.send('Hello World');
});

routerApi(app);
app.use(logErrors);
app.use(errorHandler);


app.listen(port, () => {
  console.log('Mi port' + port);
});
```
4. Actualizar products.router.js
```javascript
router.get('/:id', async (req,res, next) =>{
  try {
    const { id } = req.params;
    const product = await service.findOne(id);
    res.json(product);
  } catch (error) {
    next(error);
  }
});
```
### Manejo de errores con Boom
1. Instalar boom
```bash
 sudo npm i @hapi/boom
```
2. Actualizar error.handler.js
```javascript
function boomErrorHandler(err, req, res, next){
    if (err.isBoom) {
        const {output: {statusCode, payload}} = err;
        res.status(statusCode).json(payload);
    } else {
        next(err);
    }
}

module.exports = {logErrors, errorHandler, boomErrorHandler};
```
3. Actualizar index.js
```javascript
...

const {logErrors, errorHandler, boomErrorHandler} = require('./middlewares/error.handler');

...

routerApi(app);
app.use(logErrors);
app.use(boomErrorHandler); 
app.use(errorHandler);

...
```
4. Actualizar products.router.js
```javascript
router.post('/',async (req,res) =>{
  const body = req.body;
  const newProduct = await service.create(body);
  res.status(201).json(newProduct);
});

router.patch('/:id', async (req, res, next) => {
  try {
    const { id } = req.params;
    const body = req.body;
    const product = await service.update(id, body);
    res.json(product);
  } catch (error) {
    next(error);
  }
})
```

5. Actualizar products.service.js
```javascript
...
const boom = require('@hapi/boom');

class ProductServices {

...

    generate() {
        const limit = 100;
        for (let index = 0; index < limit; index++) {
          this.products.push({
            id: faker.datatype.uuid(),
            name: faker.commerce.productName(),
            price: parseInt(faker.commerce.price(), 10),
            image: faker.image.imageUrl(),
            isBlock: faker.datatype.boolean(),
          });
        }
      }

...

    async findOne(id) {
        const product = this.products.find(item => item.id === id);
        if (!product) {
          throw boom.notFound('product not found');
        }
        if (product.isBlock) {
          throw boom.conflict('product is block');
        }
        return product;
      }

    async update(id, changes){
        const index = this.products.findIndex(item => item.id === id);
        if (index === -1) {
            throw boom.notFound('Product not found')
        }
        const product = this.products[index];
        this.products[index] = {
            ...product,
            ...changes
        };
        return this.products[index];
    }
    
    async delete(id){
        const index = this.products.findIndex(item => item.id === id);
        if (index === -1) {
            throw boom.notFound('Product not found')
        }
        this.products.splice(index,1);
        return {id}; 
    }
}

...
```
### Validacion de datos con Joi

1. Instalar libreria
```bash
npm i joi
```
2. crear carpeta shemas/products.shema.js
```javascript
const Joi = require('joi');

const id = Joi.string().uuid();
const name = Joi.string().alphanum().min(3).max(15);
const price = Joi.number().integer().min(10);

const createProductSchema = Joi.object({
    name: name.required(),
    price: price.required(),
});

const updateProductSchema = Joi.object({
    name: name,
    price: price,
});

const getProductSchema = Joi.object({
    id: id.required(),
});

module.exports = {createProductSchema, updateProductSchema, getProductSchema};
```

3. Crear Middlewares
```javascript
const boom = require('@hapi/boom');

function validatorHandler(schema, property) {
  return (req, res, next) => {
    const data = req[property];
    const { error } = schema.validate(data);
    error ? next(boom.badRequest(error)) : next();
  };
}

module.exports = validatorHandler;
```
### Probando nuestros endpoints
[Clase](https://platzi.com/clases/2485-backend-nodejs/41761-probando-nuestros-endpoints/)

1. Actualizar products.router.js
```javascript
const express = require('express');

const ProductServices = require('../services/product.service');
const validationHandler = require('../middlewares/validator.handler');
const {createProductSchema, updateProductSchema, getProductSchema} = require('../schemas/product.schema');

...

router.get('/:id', 
  validationHandler(getProductSchema, 'params'),
  async (req,res, next) =>{
    try {
      const { id } = req.params;
      const product = await service.findOne(id);
      res.json(product);
    } catch (error) {
      next(error);
    }
  });

router.post('/',
  validationHandler(createProductSchema, 'body'),
  async (req,res) =>{
    const body = req.body;
    const newProduct = await service.create(body);
    res.status(201).json(newProduct);
  });

router.patch('/:id', 
  validationHandler(getProductSchema, 'params'),
  validationHandler(updateProductSchema, 'body'),
  async (req, res, next) => {
    try {
      const { id } = req.params;
      const body = req.body;
      const product = await service.update(id, body);
      res.json(product);
    } catch (error) {
      next(error);
    }
  });
...

```
2. Actualizar products.schema.js
```javascript
const Joi = require('joi');

const id = Joi.string().uuid();
const name = Joi.string().min(3).max(15);
const price = Joi.number().integer().min(10);
const image = Joi.string().uri();

const createProductSchema = Joi.object({
    name: name.required(),
    price: price.required(),
    image: image.required()
});

const updateProductSchema = Joi.object({
    name: name,
    price: price,
});

const getProductSchema = Joi.object({
    id: id.required(),
});

module.exports = {createProductSchema, updateProductSchema, getProductSchema};
```
3. Actualizar validator.handler.js
```javascript
const boom = require('@hapi/boom');

function validatorHandler(schema, property) {
  return (req, res, next) => {
    const data = req[property];
    const { error } = schema.validate(data, { abortEarly: false });
    error ? next(boom.badRequest(error)) : next();
  };
}

module.exports = validatorHandler;
```
### Middlewares populares en Express.js
[Documentacion](https://platzi.com/clases/2485-backend-nodejs/41762-middlewares-populares-en-expressjs/)

## Deployment










