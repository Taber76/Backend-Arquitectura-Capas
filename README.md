# Backend-Arquitectura-Capas
***
Desafio separar proyecto en capas

## Consigna
Dividir en capas el proyecto entregable con el que venimos trabajando, agrupando apropiadamente las capas de ruteo, controlador, logica de negocio y persistencia
Considerar agrupar las rutas por funcionalidad, con sus controladores, lógica de negocio con los casos de uso, y capa de persistencia.
La capa de persistencia contendra los metodos necesarios para atender la interaccion de la logica de negocio con los propios datos

## Entrega

### Descripcion general
Se ha dividido el proyecto en capas: server, ruteo, controlador/componentes y persistencia

#### Server
Se trata de un server implementado con Express que se puede ejectuar en modo 'fork' por defecto o en modo 'cluster' pasando el parametro **-m CLUSTER**, con el parametro **-p 8080** se puede indicar el puerto de escucha (en este caso 8080) y con **-a 1** se le puede indicar que para el modo cluster cada cluster escuche en un puerto distinto con numeros correlativos.
El server tambien usa **SOCKET.IO** para la carga de productos nuevos y para los mensajes de chat

#### Routes
Se han implementado dos rutas princiaples: session y api
**Session** para recibir las solicitudes de logueo, registro y deslogueo de usuario
**Api** recibe solicitudes para mostrar, editar, crear y borrar productos

#### Controlador / componentes
Al tratarse de un desarrollo sencillo esta capa se ha unificado y unicamente contiene una implemantacion de validacion de nuevo uauario o producto

#### Persistencia
Los datos son almacendados en una base de datos MongoDB, para ello se han creado clases (producto y usuario) con metodos para interactuar directamente con la base de datos.

#### Ejemplo de flujo de registro de nuevo usuario
 nuevo usuario (POST frontend) --> server (src/main.js) --> router (routes/sessionRouter.js) --> sesion de usuario (middlewares/auth.js) --> validacion (controllers/userController.js) --> persistencia (class/userContainer.js)


### Frontend
Se ha creado un frontend sencillo para interactuar con el backend

#### Login de usuario
Con la opcion de loguearse con un usuario registrado (POST || /session/login), a traves de google loguearse o registrarse (POST || /session/logingoogle) o de registrar un nuevo usuario (POST || /session/register )

### Usuario logeado 
Cuando hay un usuario logueado se muestra en el forntend un formulario de registro de nuevo producto el cual es enviado al backend mediante SOCKET