# Robotica_2023_Lab3
## Integrantes

### Wilfer Armando Fiquitiva Mendez.
### Johan Leonardo Castellanos Ruiz.
### Juan Pablo Cardenas Higuera.

## Instructivo

### Ejercicio en el laboratorio

- ** a) Familiarización con comandos de Linux **
- Como primer acercamiento a linux partimeos por conocer unos comandos como herramientas para desempeñarnos en elsistema operativo, dentro de los cuales se tiene:
-  **pwd:**Imprimir directorio de trabajo.
-  **ls:** Permite la enumeración de archivos y directorios dentro del actual.
-  **cd:** Cambiamos el directorio actual a otro que se indique.
-  **toque:**Podemos crear un archivo vacio con el nombre especificado.
-  **rm:**Eliminar archivo.
-  **mkdir:** crea un directorio.
-  **mv:** Mueve un archi o directorio a la ubicación especificada.
-  **cp:** Copia archivo o directorio.
-  **man:** Muestra la pagina del manual del comando que se especifique.
- 
- 

- **b) Conexión de ROS con Matlab**
  - **Procedimiento:**
    1. Inicia el nodo maestro con `roscore`.
    2. Ejecuta el nodo turtlesim con `rosrun turtlesim turtlesim node`.
    3. Lanza una instancia de Matlab para Linux.
    4. Crea y ejecuta un script en Matlab para controlar la tortuga.
    5. Crea un script en Matlab para suscribirse al tópico de pose de `turtle1`.
    6. Crea un script en Matlab para enviar valores asociados a la pose de `turtle1`.
    7. Consulta cómo finalizar el nodo maestro en Matlab.
**Resultados**
Se instalaron los servicios de matlab y ros en las terminales con linux y con windows
![Punto b posicion inicial](https://github.com/jcardenash99/Robotica_2023_Lab3/assets/61796945/06fea9a2-5530-4a0d-b5f2-e000b2d00073)

Se ejecuto en la terminal con linux en dos instancias los comandos `roscore` y `rosrun turtlesim turtlesim node`. Al realizar esto aparece una ventana con la simulación de una tortuga.\n
Para desplazar la tortuga y ver su posicion se crearon los codigos de matlab para las dos terminales.

Codigo en matlab en la terminal con windows
```matlab
 %cierra o apaga el nodo en el matlab de windows
 %rosshutdown; 
 %inicializa el nodo en matlab de windows tomando 
 %como maestro el nodo en linux (por su ip)
 %rosinit('192.168.1.xx');
 %Crea una suscripcion al mensage que publica el nodo maestro dnde publica
 %la velocidad lineal y el angulo del nodo
 Subcriber=rossubscriber('/turtle1/cmd_vel','geometry_msgs/Twist');
 %crea una suscripcion a la pose del nodo turtlesim
 Pose=rossubscriber("/turtle1/pose");
 %pausa el codigo para dar tiempo de espera al mensaje
 pause(2)
 %guardamos el ultimo mensaje publicado por los nodos
 LastMesage=Subcriber.LatestMessage;
 LastPose=Pose.LatestMessage;
 
 %guarda los valores de la pose en variables para su vizualizacion
 pose_x=LastPose.X
 pose_y=LastPose.Y
 pose_theta=LastPose.Theta
 
 pose_vel=LastPose.LinearVelocity
 pose_angVel=LastPose.AngularVelocity
 
 pause(1)
```
Codigo de matlab en la terminal con linux (siendo esta el nodo maestro)
```matlab
 %apaga la instacia al nodo de matlab en linux
 %rosshutdown;
 %inicia la instancia al nodo de matlab en linux por defecto
 %rosinit; 
 %crea el publisher del desplazamiento de la tortuga en matlab
 velPub = rospublisher('/turtle1/cmd_vel','geometry_msgs/Twist'); %Creacion publicador
 velMsg = rosmessage(velPub); %Creacion de mensaje
 %cambiar los valores a publicar
 velMsg.Linear.X = 2; %desplazamiento linear en x
 velMsg.Linear.Y = -1;%desplazamiento linear en y
 velMsg.Angular.Z = pi; %rotacion linear en z
 send(velPub,velMsg); %Envio del mensaje
 pause(1)
```
Estos codigos son los codigos respectivos para las dos terminales una siendo la que publica (terminal con linux) la otra siendo la que se suscribe (terminal con windows). \n
Como Se observa en la figura, tenemos la tortuga en la posicion inicial, esta es en X=5.544 Y=5.544 Z=0. \n
![Posicion inicial](https://github.com/jcardenash99/Robotica_2023_Lab3/assets/61796945/49845027-dcc4-4ac4-876a-362587bf2c4a)
![Datos de la posicion inicial](https://github.com/jcardenash99/Robotica_2023_Lab3/assets/61796945/026fdde4-01f2-4a63-bb19-f2c9b4153c77)

Al ejecutar un cambio en la posción inicial en la terminal en linux tenemos un desplazamiento en la grafica, y al ejecutar el codigo en matla en linux se observa la poscion de la tortuga.
![Primer desplazamiento](https://github.com/jcardenash99/Robotica_2023_Lab3/assets/61796945/a98b4cbf-07c2-49ec-82ee-377994f7a39e)
![Primer desplazamiento pose](https://github.com/jcardenash99/Robotica_2023_Lab3/assets/61796945/a204cdfd-7826-4e81-977a-56aea39d0e0f)

Como podemos observar en el codigo en linux se realiza al tiempo un desplazamiento en `x=2 y=-1 theta=z=pi` se dezplaza la tortuga y en windows en el codigo de matlab se puede observar la posicion final (actual en la que se encuentra la tortuga).\n
Finalmente para terminar las 2 instancias de los nodos en matlab usamos el comando `rosshutdown`.
- **c) Utilizando Python**
  - **Procedimiento para operar una tortuga con el teclado:**
    - Mover la tortuga hacia adelante y hacia atrás con las teclas W y S.
    - Girar en sentido horario y antihorario con las teclas D y A.
    - Retornar a la posición y orientación centrales con la tecla R.
    - Realizar un giro de 180° con la tecla ESPACIO.
  - Incluye el script en la sección de `catkin install python` del archivo `CMakeLists.txt`.
  - Compila el paquete modificado con `catkin`.
  - Ejecuta el script en una terminal para controlar la tortuga con el teclado.
