# Robotica_2023_Lab3
## Integrantes

### Wilfer Armando Fiquitiva Mendez.
### Johan Leonardo Castellanos Ruiz.
### Juan Pablo Cardenas Higuera.

## Instructivo de Actividad

### Ejercicio en el laboratorio

- **a) Familiarización con comandos de Linux**
  - Familiarízate con los comandos de mayor uso para la consola de Linux. Puedes encontrar más información en [este enlace](http://www.informit.com/blogs/blog.aspx?uk=The-10-Most-Important-Linux-Commands).

- **b) Conexión de ROS con Matlab**
  - **Procedimiento:**
    1. Inicia el nodo maestro con `roscore`.
    2. Ejecuta el nodo turtlesim con `rosrun turtlesim turtlesim node`.
    3. Lanza una instancia de Matlab para Linux.
    4. Crea y ejecuta un script en Matlab para controlar la tortuga.
    5. Crea un script en Matlab para suscribirse al tópico de pose de `turtle1`.
    6. Crea un script en Matlab para enviar valores asociados a la pose de `turtle1`.
    7. Consulta cómo finalizar el nodo maestro en Matlab.

- **c) Utilizando Python**
  - **Procedimiento para operar una tortuga con el teclado:**
    - Mover la tortuga hacia adelante y hacia atrás con las teclas W y S.
    - Girar en sentido horario y antihorario con las teclas D y A.
    - Retornar a la posición y orientación centrales con la tecla R.
    - Realizar un giro de 180° con la tecla ESPACIO.
  - Incluye el script en la sección de `catkin install python` del archivo `CMakeLists.txt`.
  - Compila el paquete modificado con `catkin`.
  - Ejecuta el script en una terminal para controlar la tortuga con el teclado.
