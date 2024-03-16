
# Desplegar API basada en NodeJS con AWS Lambda y API Gateway conectada a DynamoDB.
En este repositorio veremos paso a paso como crear una API que contiene las operaciones CRUD a una base de datos en DynamoDB con AWS Lambda en NodeJS y su despliegue para consumo a través de AWS API Gateway. 

## 💻 Requerimientos
- Usuario de consola AWS (con permisos para api gateway y lambda)

## 📝 Paso a paso

### Paso 1: Creación de la base de datos en DynamoDB.
1.1 Entrar a DynamoDB desde la consola de AWS

1.2 Clic en crear tabla

1.3 Agregar nombre de la tabla, para la demo será: demo_api_dynamodb

1.4 Agregar clave de partición (primary key), para este repositorio será: id, de tipo cadena

1.5 Clic en crear tabla

1.6 Una vez que la tabla este activa, entramos a crear elementos dando clic sobre la tabla

1.7 Clic sobre explorar elementos, seguido de crear elemento

1.8 Añadimos un elemento conformado por:

```json
{
  "id": "1",
  "email": "abenitez@mail.com",
  "name": "Ana Benitez"
}
```
1.9 Clic en crear elemento

¡Tenemos base de datos con al menos un registro para su consulta!

### Paso 2: Creación del Lambda con NodeJS.

2.1 Entrar a AWS Lambda desde la consola de AWS

2.2 Clic en crear una función

2.3 Seleccionamos Crear desde cero
 
2.4 Le damos un nombre: demo_api_lambda

2.5 En el valor de tiempo de ejecución seleccionamos: NodeJS 20.x

2.6 En el apartado de Configuración avanzada añadimos el permiso para DynamoDB, damos seleccionamos Creación de un nuevo rol desde la política de AWS Templates

2.7 Agregamos el nombre: demo_api_rol_dynamodb

2.8 Seleccionamos en plantilla de política: Permisos de microservicios sencillos

2.9 Clic en crear función

2.10 Se va a crear la lambda, en la parte ce código, copia y pega el contendio del archivo demo_api_lambda.js, el cual contiene el código en NodeJS con las operaciones CRUD del API

```
GET /users  -->  Consulta de todos los usuarios
GET /users/{id} -->  Consulta por id del usuario
PUT /users  --> Creación/actualización completa de la información del usuario
DELETE /users/{id}  -->  Eliminación del usuario por su id
```

2.11 Clic en Deploy

¡Tenemos nuestra función lambda con código NodeJS que se conecta a nuestra base de datos en DynamoDB!

**NOTA:** si cambiaste el nombre de la tabla asegúrate de actualizar el código antes de desplegar.

### Paso 3: Creación y configuración del API Gateway.

3.1 Entrar a Amazon API Gateway desde la consola de AWS

3.2 Clic en Crear, sobre API HTTP

3.3 Clic sobre Agregar integración, seleccionar lambda y en función lambda, buscar la que acabamos de crear en el paso 2

3.4 Agregar nombre del API: demo_api_gateway

3.5 Clic en siguiente

3.6 Seleccionar el método, ruta y destino por cada recurso que posee nuestra API:

| Método    | Ruta de acceso | Destino de integración |
|-----------|----------------|------------------------|
| GET       | /users         | demo_api_lambda        |
| GET       | /users/{id}    | demo_api_lambda        |
| PUT       | /users         | demo_api_lambda        |
| DELETE    | /users/{id}    | demo_api_lambda        |


3.7 Clic en siguiente

3.8 Agregar nombre de la etapa, en este caso: dev

3.9 Clic en siguiente

3.10 Revisamos el resumen y clic en Crear

¡Listo! Ya tenemos nuestra API lista para ser consumida desde un endpoint que posee el CRUD de usuarios en una base de datos en DynamoDB a través de la implementación de un Lambda con NodeJS.

### Paso 4: Pruebas unitarias.

4.1 Podremos regresar a nuestro lambda, en la sección de Configuración, Desencadenadores veremos el endpoint generado (si no lo visualizas, solo refresca la sección)

4.2 Con el endpoint disponible, utiliza tu cliente HTTP de confianza y genera un set de pruebas unitarias para probar cada recurso del API


## 📚 Documentación

Artículo completo en [Medium](https://medium.com/@brendagalicia/desplegar-api-basada-en-nodejs-con-aws-lambda-y-api-gateway-conectada-a-dynamodb-d4c5fd4f5748).

## 🎬 Demo

Video completo de la demo en [YouTube](https://youtu.be/4tqsuJmRskU).
