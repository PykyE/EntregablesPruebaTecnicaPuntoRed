# Entrega documentación prueba técnica Punto Red
 
## Instrucciones de uso

### Nivel 0 (Api Spring Boot)

1) Configurar las siguientes variables de entorno en el entorno de desarrollo que se utilice

- `baseUrl` : Url del API de punto red provista en la documentación
- `db_host` : Host de la base de datos
- `db_name` : Nombre de la base de datos
- `db_username` : Nombre de usuario de la base de datos
- `db_password` : Contraseña de usuario de la base de datos
- `username` : Nombre de usuario para solicitar el token de autenticación
- `password` : Contraseña de usuario para solicitar el token de autenticación

2) Ejecutar la API (Haciendo uso del IDE o el CLI del gestor de paquetes maven)

3) Dentro de la API se podrán encontrar los siguientes endpoints

- `/supplier` : Endpoint para peticiones GET, en donde se devolverán los proveedores disponibles desde la API de punto red.
- `/transaction` : Endpoint para peticiones GET y POST, con el primer método se devolveran las transacciones almacenadas en la base de datos, y con el segundo método se realizará una recarga en el endpoint designado de la API de punto red, devolviendo un ticket de confirmación de la transferencia e insertando un nuevo registro de transacción en la base de datos.

### Nivel 1 (Script base de datos postgreSQL)

1) Ejecutar el script dado (Ya sea en una plataforma de administración o CLI de PostgreSQL)
2) Se contará con una tabla llamada *Transactions* que constará de la siguiente estrucutra

- `id` : Id único de la operación
- `date` : Fecha con zona horaria de la recarga
- `amount` : Cantidad recargada
- `clientTransId` : Id del cliente
- `phoneNumber` : Número telefónico
- `supplierId` : Id del proveedor de la recarga

3) Estos atributos cuentan con las restricciones dadas en la documentación al ejecutar el script dado

### Nivel 2 (Página web)

1) Ubicarse en la raiz del proyecto e instalar los `node_modules` usando el comando `npm install`
2) Ejecutar la página con el comando `npm run dev`

### Notas

1) El contenido del body para la petición POST al endpoint `/transaction` deberá tener la siguiente estrucutra

- `clientTransId` : Id del cliente
- `amount` : Cantidad a recargar
- `phoneNumber` : Número telefónico
- `supplierId` : Id del proveedor de la recarga

2) Para el apartado de frontend de ser posible configurar en el entorno de desarrollo utilizado la variable `baseUrl` 
y asignarle el valor de la url de la API de Spring Boot dada, y referirla en el archivo `axios.js` del paquete `Connection`

3) La página web correrá sobre el puerto 8081 por defecto, esto se puede cambiar si se desea en el archivo `webpack.config.js`

4) Pueden darse ocasiones en donde las peticiones POST al endpoint `/transaction` y las peticiones GET al endpoint `/supplier`
devuelvan un error 500 o 503, esto dado que la configuración interna del API de Spring Boot no está completamente sincronizada/configurada
con los tiempos de respuesta de la API provista de punto red, esto puede ser un punto de mejora en el futuro
