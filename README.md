
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

# Investigar acerca de la vista en MVC

## Vistas en las cuales se reciben y envían los datos del modelo y los muestra al usuario.  

Vista: es el interfaz de usuario, que muestra los datos del modelo, El frontend o interfaz gráfica de usuario.
### ¿Por qué deberías usar MVC?

El patrón MVC te ayuda a dividir el código frontend y backend en componentes separados. De esta manera, es mucho más fácil administrar y hacer cambios a cualquiera de los lados sin que interfieran entre sí. Es mas facil usarlo cuando varios desarrolladores necesitan actualizar, modificar o depurar una aplicación completada simultáneamente.

![Imagen Vista](https://www.freecodecamp.org/espanol/news/content/images/size/w1600/2021/06/MVC3.png)

## Ejemplo

Como ejemplo vamos a poner una tienda de carros donde el usuario ver la pagina en su pantalla.

La aplicación "Car Clicker" tiene dos vistas: carListView y CarView.

1-CarListView
~~~
const carListView = {
    init() {
        // almacene el elemento DOM para un fácil acceso más tarde
        this.carListElem = document.getElementById('car-list');

        // renderizar esta vista (actualizar los elementos DOM con los valores correctos)
        this.render();
    },

    render() {
        let car;
        let elem;
        let i;
        // obtener los carros para ser renderizados desde el controlador
        const cars = controller.getCars();

        // para asegurarse de que la lista está vacía antes de renderiz
        this.carListElem.innerHTML = '';

        // bucle sobre el arreglo de carros
        for(let i = 0; i < cars.length; i++) {
            // este es el carro que tenemos en bucle
            car = cars[i];

            // hacer un nuevo elemento de la lista de carros y establecer su texto
            elem = document.createElement('li');
            elem.className = 'list-group-item d-flex justify-content-between lh-condensed';
            elem.style.cursor = 'pointer';
            elem.textContent = car.name;
            elem.addEventListener(
                'click',
                (function(carCopy) {
                    return function() {
                        controller.setCurrentCar(carCopy);
                        carView.render();
                    };
                })(car)
            );
            // finalmente, agregua el elemento a la lista
            this.carListElem.appendChild(elem);
        }
    },
};
~~~
2-CarView
~~~
const carView = {
    init() {
        // almacene punteros a los elementos DOM para un fácil acceso más tarde
        this.carElem = document.getElementById('car');
        this.carNameElem = document.getElementById('car-name');
        this.carImageElem = document.getElementById('car-img');
        this.countElem = document.getElementById('car-count');
        this.elCount = document.getElementById('elCount');


        // al hacer clic, aumentar el contador del carro actual
        this.carImageElem.addEventListener('click', this.handleClick);

        // renderizar esta vista (actualizar los elementos DOM con los valores correctos)
        this.render();
    },

    handleClick() {
    	return controller.incrementCounter();
    },

    render() {
        // actualizar los elementos DOM con valores del carro actual
        const currentCar = controller.getCurrentCar();
        this.countElem.textContent = currentCar.clickCount;
        this.carNameElem.textContent = currentCar.name;
        this.carImageElem.src = currentCar.imgSrc;
        this.carImageElem.style.cursor = 'pointer';
    },
};
~~~

![imagen vista](https://www.freecodecamp.org/news/content/images/2021/04/Screen-Recording-2021-04-11-at-11.31.27.07-PM.gif)

## BIBLIOGRAFIA

- http://www.jtech.ua.es/j2ee/2004-2005/modulos/jsp/sesion06-apuntes.htm#:~:text=Vista%3A%20es%20el%20interfaz%20de%20usuario%2C%20que%20muestra,en%20el%20modelo%20y%20muestra%20la%20vista%20correspondiente.

- https://www.freecodecamp.org/espanol/news/el-modelo-de-arquitectura-view-controller-pattern/ 

# Investigar acerca del controlador en MVC

## Identificar los eventos necesarios que cumplan con la lógica del negocio.

Contiene el **código necesario para responder a las acciones que se solicitan** en la aplicación, como visualizar un elemento, realizar una compra, una búsqueda de **información**, etc.
Se resume en que él controlador tiene la información.

![Imagen controlador](https://desarrolloweb.com/archivoimg/general/2758.jpg)

La **"lógica de aplicación / negocio"**, que es algo que pertenece a los controladores. Por ejemplo, cuando me piden ver el resumen de **datos de un usuario**. Esa acción le llega al controlador, que tendrá que acceder al **modelo del usuario para pedir sus datos**. Luego llamará a la **vista apropiada para poder mostrar esos datos del usuario**. Si en el resumen del usuario queremos mostrar los artículos que ha publicado dentro de la aplicación, quizás el controlador **tendrá que llamar al modelo de artículos**, pedirle todos los publicados por ese usuario y con ese listado de artículos **invocar a la vista correspondiente para mostrarlos**. 

![Imagen controlador](https://possibleapp.com/blog/wp-content/uploads/2016/01/MVC-720x380.png)

## Ejemplo

Con el ejemplo anterior de los carros vamos a ver el controlador de este mismo. Pues el controlador es el cerebro. 
~~~
const controller = {
    init() {
        // establecer el carro actual como el primero en la lista
        model.currentCar = model.cars[0];

        // indicar a las vistas que inicialicen
        carListView.init();
        carView.init();
    },

    getCurrentCar() {
    	return model.currentCar;
    },

    getCars() {
    	return model.cars;
    },

    // establecer el carro seleccionado actualmente en el objeto que se pasa en
    setCurrentCar(car) {
    	model.currentCar = car;
    },

    // incrementar el contador para el coche seleccionado actualmente
    incrementCounter() {
        model.currentCar.clickCount++;
        carView.render();
    },
};

controller.init();
~~~

## BIBLIOGRAFIA

- https://desarrolloweb.com/articulos/que-es-mvc.html

- https://www.freecodecamp.org/espanol/news/el-modelo-de-arquitectura-view-controller-pattern/

- ESTEFANIA JAIDE ROSAS RAMIREZ
