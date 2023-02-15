
# Modelo-vista-controlador

**MVC** Es un patrón de diseño de software que divide el programa o la aplicación web relacionada en tres elementos o componentes interconectados. Cada uno de estos componentes se construye para manejar aspectos específicos de desarrollo de una aplicación.

![Imagen](https://codigofacilito.com/photo_generales_store/29.jpg)

## Representacion de datos

Con esta representacion, las solicitudes del usuario se enrutan a un controlador que se encarga de trabajar con el modelo para realizar las acciones del usuario o recuperar los resultados de consultas. 
- El controlador elige la vista para mostrar al usuario y proporciona cualquier dato de modelo que sea necesario.

## Funcionalidades de la aplicación

- 1: El usuario interactúa con la interfaz de usuario de alguna forma (por ejemplo, el usuario pulsa un botón, enlace, etc.)
- 2: El **controlador** delega a los objetos de la vista la tarea de desplegar la interfaz de usuario. 
- La **vista** obtiene sus datos del modelo para generar la interfaz apropiada para el usuario donde se refleja los cambios en el modelo (por ejemplo, produce un listado del contenido del carro de la compra).
- El **modelo** no debe tener conocimiento directo sobre la vista. Sin embargo, se podría utilizar el patrón Observador para proveer cierta indirección entre el modelo y la vista, permitiendo al modelo notificar a los interesados de cualquier cambio. Un objeto vista puede registrarse con el modelo y esperar a los cambios, pero aun así el modelo en sí mismo sigue sin saber nada de la vista. El controlador no pasa objetos de dominio (el modelo) a la vista aunque puede dar la orden a la vista para que se actualice.
- 3: La interfaz de usuario espera nuevas interacciones del usuario, comenzando el ciclo nuevamente.
 
## Infraestructura y recuperación de datos

Consiste en un patrón de diseño de software que se utiliza para separar en tres componentes los datos, la metodología y la interfaz gráfica de una aplicación. La gran ventaja que posee esta técnica de programación es que permite **modificar** cada uno de ellos sin necesidad de modificar los demás, lo que permite desarrollar aplicaciones modulares y escalables que se puedan **actualizar fácilmente** y añadir o eliminar nuevos módulos.

![Imagen](https://th.bing.com/th/id/R.0810521a14def63df7e4bab289041f84?rik=ps0RfRT3op2PlQ&riu=http%3a%2f%2f3.bp.blogspot.com%2f-PxF_DYMJ46I%2fUY5WWbZWI6I%2fAAAAAAAAB3w%2ftSB-t2pDw3c%2fs1600%2fMVC.png&ehk=SnkMXnR5hZR6LGultsAWAWMTTpyhjgSq9av9f2FOKb8%3d&risl=&pid=ImgRaw&r=0)

## Ejemplos:

### **VISTA**
~~~
<html>
   <head>
      <title>LIBRERIA UAZON</title>
   </head>
   <body>
     <h1>Libros dados de alta en nuestra libreria</h1>
     <table border="1">
        <tr>
           <th>TITULO</th>
           <th>PRECIO</th>
        </tr>
~~~
![Imagen](https://mcazorla.gitbooks.io/programacion-en-el-servidor/content/php14-frontcontroller.png)

### **MODELO**
~~~
<?php
   $db = new PDO('mysql:host=localhost;dbname=uazon', 'comprador', 'proweb2013');
   $result = $db->query('SELECT titulo, precio FROM libros');
   while ($libro = $result->fetch()) { }
function getLibro($id)
{
   $db = getConnection();
   $query = 'SELECT * FROM libros WHERE id = ?';
   $stmt = $db->prepare($query);
   $stmt->execute(array($id));
   $libro = $stmt->fetch();
   return $libro;
}
?>
~~~
### **CONTROLADOR**
~~~
<?php
   // modelo
   require 'model.php';
   // un array con todos los libros del modelo
   //La vista recibe un array para mostrarlo por pantalla
   include 'view.php';
?>
function ver ()
{
   if ( !isset ( $_GET [ 'id' ] ) )
      die("No has especificado un identificador de libro.");
   $id = $_GET [ 'id' ];
   //Incluimos el modelo
   require 'models/libros_model.php';
   //Le pide al modelo el libro con id = $id
   $libro = getLibro($id);
   if ($libro === null)
      die("Identificador de libro incorrecto");
   //Pasamos a la vista toda la información que se desea representar
   include('views/libros_ver.php');
}
~~~

## BIBLIOGRAFIA

- https://mcazorla.gitbooks.io/programacion-en-el-servidor/content/patrones_de_diseno_en_php_ii__patron_mvc/ejemplo_de_como_crear_un_sistema_mvc_paso_a_paso_1.html

- https://si.ua.es/es/documentacion/asp-net-mvc-3/1-dia/modelo-vista-controlador-mvc.html#:~:text=El%20controlador%20delega%20a%20los%20objetos,datos%20del%20modelo%20a%20la%20vista.&text=El%20controlador%20delega%20a,modelo%20a%20la%20vista.&text=delega%20a%20los%20objetos,datos%20del%20modelo%20a

ESTEFANIA JAIDE ROSAS RAMIREZ 