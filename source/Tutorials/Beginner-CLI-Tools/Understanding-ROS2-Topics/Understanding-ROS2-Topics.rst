.. redirect-from::

    Tutorials/Topics/Understanding-ROS2-Topics

.. _ROS2Topics:

Comprender los Topics
=====================

**Objetivo:** Utilizar rqt_graph y las herramientas de línea de comandos para inspeccionar los topics de ROS 2.

**Nivel del Tutorial:** Principiante

**Tiempo:** 20 minutos

.. contents:: Contenido
   :depth: 2
   :local:

Historial
---------

ROS 2 divide los sistemas complejos en muchos nodos modulares.
Los topic son un elemento vital del grafo de ROS, que actúa como un bus para que los nodos intercambien mensajes.

.. image:: images/Topic-SinglePublisherandSingleSubscriber.gif

Un nodo puede publicar datos en cualquier número de topics y simultáneamente tener suscripciones a cualquier número de topics.

.. image:: images/Topic-MultiplePublisherandMultipleSubscriber.gif

Los topics son una de las principales formas en que los datos se mueven entre nodos y, por lo tanto, entre diferentes partes del sistema.


Requisitos previos
------------------

El :doc:`tutorial previo <../Understanding-ROS2-Nodes/Understanding-ROS2-Nodes>` proporciona información básica sobre los nodos que se construyen aquí.

<<<<<<< HEAD
Como siempre, no olvides ejecutar `source` con el archivo de setup :doc:`en cada nueva terminal<../Configuring-ROS2-Environment>`.
=======
As always, don't forget to source ROS 2 in :doc:`every new terminal you open <../Configuring-ROS2-Environment>`.
>>>>>>> og

Tareas
------

1 Configuración
^^^^^^^^^^^^^^^

A estas alturas ya deberías estar cómodo iniciando Turtlesim.

Abre una nueva terminal y ejecuta:

.. code-block:: console

    ros2 run turtlesim turtlesim_node

Abre otra terminal y ejecuta:

.. code-block:: console

    ros2 run turtlesim turtle_teleop_key

Recuerde del :doc:`tutorial previo <../Understanding-ROS2-Nodes/Understanding-ROS2-Nodes>` que los nombres de estos nodos son ``/turtlesim`` y ``/teleop_turtle`` por defecto.

2 rqt_graph
^^^^^^^^^^^

A lo largo de este tutorial, utilizaremos ``rqt_graph`` para visualizar los nodos y topics cambiantes, así como las conexiones entre ellos.

El tutorial :doc:`turtlesim <../Introducing-Turtlesim/Introducing-Turtlesim>` indica cómo instalar rqt y todos sus complementos, incluido ``rqt_graph``.

Para ejecutar rqt_graph, abre una nueva terminal e ingrese el comando:

.. code-block:: console

    rqt_graph

También puedes abrir rqt_graph abriendo ``rqt`` y seleccionando **Plugins** > **Introspection** > **Node Graph**.

.. image:: images/rqt_graph.png

Deberías ver los nodos (elipses) y los topic (rectángulo) como en la imágen anterior.
También se pueden observar dos acciones alrededor de la periferia del gráfico (ignorémoslas por ahora).
Si pasas el mouse sobre el topic en el centro, verá el color resaltado como en la imagen de arriba.

El gráfico muestra cómo el nodo ``/turtlesim`` y el nodo ``/teleop_turtle`` se comunican entre sí mediante un topic.
El nodo ``/teleop_turtle`` está publicando datos (las pulsaciones de teclas que introduce para mover la tortuga) en el topic ``/turtle1/cmd_vel``, y el nodo ``/turtlesim`` está suscrito a ese topic para recibir los datos.

La característica de resaltado de rqt_graph es muy útil cuando se examinan sistemas más complejos con muchos nodos y topics conectados de muchas maneras diferentes.

<<<<<<< HEAD
Como vimos recién, rqt_graph es una herramienta gráfica de inspección.
Ahora veremos algunas herramientas de línea de comandos para la inspección de topics.
=======
rqt_graph is a graphical introspection tool.
Now we'll look at some command line tools for introspecting topics.
>>>>>>> og


3 ros2 topic list
^^^^^^^^^^^^^^^^^

Ejecuta el comando ``ros2 topic list`` en una nueva terminal para obtener una lista de todos los topics actualmente activos en el sistema:

.. code-block:: console

  /parameter_events
  /rosout
  /turtle1/cmd_vel
  /turtle1/color_sensor
  /turtle1/pose

``ros2 topic list -t`` devolverá la misma lista de topics, esta vez con el tipo entre corchetes:

.. code-block:: console

  /parameter_events [rcl_interfaces/msg/ParameterEvent]
  /rosout [rcl_interfaces/msg/Log]
  /turtle1/cmd_vel [geometry_msgs/msg/Twist]
  /turtle1/color_sensor [turtlesim/msg/Color]
  /turtle1/pose [turtlesim/msg/Pose]

<<<<<<< HEAD
Estos atributos, particularmente el tipo, son la forma en que los nodos saben que están hablando de la misma información a medida que se mueve sobre los topics.

Si te preguntas dónde están todos estos topics en rqt_graph, puedes desmarcar todas las casillas debajo de **Hide**:
=======
These attributes, particularly the type, are how nodes know they're talking about the same information as it moves over topics.

If you're wondering where all these topics are in rqt_graph, you can uncheck all the boxes under **Hide:**
>>>>>>> og

.. image:: images/unhide.png

Por ahora, deja esas opciones marcadas para evitar confusiones.

4 ros2 topic echo
^^^^^^^^^^^^^^^^^

Para ver los datos que se publican sobre un topic, utiliza:

.. code-block:: console

    ros2 topic echo <topic_name>

<<<<<<< HEAD
Como sabemos que ``/teleop_turtle`` publica datos en ``/turtlesim`` sobre el topic ``/turtle1/cmd_vel``, utilizaremos ``echo`` para hacer una inspección sobre ese topic:
=======
Since we know that ``/teleop_turtle`` publishes data to ``/turtlesim`` over the ``/turtle1/cmd_vel`` topic, let's use ``echo`` to introspect that topic:
>>>>>>> og

.. code-block:: console

    ros2 topic echo /turtle1/cmd_vel

<<<<<<< HEAD
Al principio, este comando no devolverá ningún dato.
Eso es porque está esperando que ``/teleop_turtle`` publique algo.

Regresa a la terminal donde se está ejecutando ``turtle_teleop_key`` y usa las flechas para mover la tortuga.
Si observas la terminal donde se ejecuta el comando ``echo``, verás que se publican los datos de posición para cada movimiento que realice:
=======
At first, this command won't return any data.
That's because it's waiting for ``/teleop_turtle`` to publish something.

Return to the terminal where ``turtle_teleop_key`` is running and use the arrows to move the turtle around.
Watch the terminal where your ``echo`` is running at the same time, and you'll see position data being published for every movement you make:
>>>>>>> og

.. code-block:: console

  linear:
    x: 2.0
    y: 0.0
    z: 0.0
  angular:
    x: 0.0
    y: 0.0
    z: 0.0
    ---

Ahora regresa a rqt_graph y desmarque la casilla **Debug**.

.. image:: images/debug.png

<<<<<<< HEAD
``/_ros2cli_26646`` es el nodo creado por el ``echo`` que acabamos de ejecutar (el número puede ser diferente).
Ahora puedes ver que el editor está publicando datos sobre el topic ``cmd_vel`` y que hay dos suscriptores suscritos.
=======
``/_ros2cli_26646`` is the node created by the ``echo`` command we just ran (the number might be different).
Now you can see that the publisher is publishing data over the ``cmd_vel`` topic, and two subscribers are subscribed to it.
>>>>>>> og

5 ros2 topic info
^^^^^^^^^^^^^^^^^

<<<<<<< HEAD
Los topics no tienen que ser solo comunicación punto a punto; puede ser de uno a muchos, de muchos a uno o de muchos a muchos.
=======
Topics don't have to only be one-to-one communication; they can be one-to-many, many-to-one, or many-to-many.
>>>>>>> og

Otra forma de ver esto es ejecutando:

.. code-block:: console

    ros2 topic info /turtle1/cmd_vel

Que devolverá:

.. code-block:: console

  Type: geometry_msgs/msg/Twist
  Publisher count: 1
  Subscription count: 2

6 ros2 interface show
^^^^^^^^^^^^^^^^^^^^^

Los nodos envían datos sobre topics mediante mensajes.
Los Publicadores y Suscriptores deben enviar y recibir el mismo tipo de mensaje para comunicarse.

Los tipos de topics que vimos antes, después de ejecutar ``ros2 topic list -t`` nos permiten saber qué tipo de mensaje se usa en cada topic.
Recuerda que el topic ``cmd_vel`` tiene el tipo:

.. code-block:: console

    geometry_msgs/msg/Twist

Esto significa que en el paquete ``geometric_msgs`` hay un ``mensaje`` llamado ``Twist``.

<<<<<<< HEAD
Ahora podemos ejecutar ``ros2 interface show <msg type>`` con el tipo de mensaje anterio para conocer sus detalles, específicamente, qué estructura de datos espera el mensaje.
=======
Now we can run ``ros2 interface show <msg type>`` on this type to learn its details.
Specifically, what structure of data the message expects.
>>>>>>> og

.. code-block:: console

    ros2 interface show geometry_msgs/msg/Twist

Para el tipo de mensaje de arriba, produce:

.. code-block:: console

  # This expresses velocity in free space broken into its linear and angular parts.

      Vector3  linear
              float64 x
              float64 y
              float64 z
      Vector3  angular
              float64 x
              float64 y
              float64 z

<<<<<<< HEAD
Esto indica que el nodo ``/turtlesim`` está esperando un mensaje con dos vectores, ``linear`` y ``angular``, de tres elementos cada uno.
Si recuerdas los datos que vimos pasar de ``/teleop_turtle`` a ``/turtlesim`` con el comando ``echo``, utilizan la misma estructura:
=======
This tells you that the ``/turtlesim`` node is expecting a message with two vectors, ``linear`` and ``angular``, of three elements each.
If you recall the data we saw ``/teleop_turtle`` passing to ``/turtlesim`` with the ``echo`` command, it's in the same structure:
>>>>>>> og

.. code-block:: console

  linear:
    x: 2.0
    y: 0.0
    z: 0.0
  angular:
    x: 0.0
    y: 0.0
    z: 0.0
    ---

7 ros2 topic pub
^^^^^^^^^^^^^^^^

Ahora que tienes la estructura del mensaje, puedes publicar datos en un topic directamente desde la línea de comando usando:

.. code-block:: console

    ros2 topic pub <topic_name> <msg_type> '<args>'

<<<<<<< HEAD
El argumento ``'<args>'`` son los datos que pasarán al topic, en la estructura que acabas de utilizar en la sección anterior.

Es importante tener en cuenta que este argumento se debe introducir utilizando la sintaxis YAML.
Ingrese el comando completo así:
=======
The ``'<args>'`` argument is the actual data you'll pass to the topic, in the structure you just discovered in the previous section.

It's important to note that this argument needs to be input in YAML syntax.
Input the full command like so:
>>>>>>> og

.. code-block:: console

  ros2 topic pub --once /turtle1/cmd_vel geometry_msgs/msg/Twist "{linear: {x: 2.0, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: 1.8}}"

``--once`` es un argumento opcional que significa "publicar un mensaje y luego salir".

<<<<<<< HEAD
Recibirás el siguiente mensaje en la terminal:
=======
You will see the following output in the terminal:
>>>>>>> og

.. code-block:: console

  publisher: beginning loop
  publishing #1: geometry_msgs.msg.Twist(linear=geometry_msgs.msg.Vector3(x=2.0, y=0.0, z=0.0), angular=geometry_msgs.msg.Vector3(x=0.0, y=0.0, z=1.8))

Y verás a tu tortuga moverse así:

.. image:: images/pub_once.png

La tortuga (y comúnmente los robots reales que pretende emular) requieren un flujo constante de comandos para operar continuamente.
Entonces, para que la tortuga siga moviéndose, puedes ejecutar:

.. code-block:: console

  ros2 topic pub --rate 1 /turtle1/cmd_vel geometry_msgs/msg/Twist "{linear: {x: 2.0, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: 1.8}}"

La diferencia aquí es la eliminación de la opción ``--once`` y la adición de la opción ``--rate 1``, que le dice a ``ros2 topic pub`` que publique el comando en un flujo constante a 1 Hz.

.. image:: images/pub_stream.png

<<<<<<< HEAD
Puedes actualizar rqt_graph para ver lo que sucede gráficamente.
Verás que el nodo ``ros 2 topic pub ...`` (``/_ros2cli_30358``) se está publicando sobre el topic ``/turtle1/cmd_vel``, y lo está recibiendo tanto el nodo ``ros2 topic echo ...`` (``/_ros2cli_26646``) como el nodo ``/turtlesim``.
=======
You can refresh rqt_graph to see what's happening graphically.
You will see that the ``ros2 topic pub ...`` node (``/_ros2cli_30358``) is publishing over the ``/turtle1/cmd_vel`` topic, which is being received by both the ``ros2 topic echo ...`` node (``/_ros2cli_26646``) and the ``/turtlesim`` node now.
>>>>>>> og

.. image:: images/rqt_graph2.png

Finalmente, puedes ejecutar ``echo`` en el topic de ``pose`` y volver a verificar rqt_graph:

.. code-block:: console

  ros2 topic echo /turtle1/pose

.. image:: images/rqt_graph3.png

<<<<<<< HEAD
Puedes ver que el nodo ``/turtlesim`` también está publicando en el topic de ``pose``, al que está suscrito el nuevo nodo de ``echo``.
=======
You can see that the ``/turtlesim`` node is also publishing to the ``pose`` topic, which the new ``echo`` node has subscribed to.
>>>>>>> og

8 ros2 topic hz
^^^^^^^^^^^^^^^

Para una última inspección sobre este proceso, puedes ver la velocidad a la que se publican los datos usando:

.. code-block:: console

    ros2 topic hz /turtle1/pose

Devolverá datos sobre la velocidad a la que el nodo ``/turtlesim`` está publicando datos en el topic de ``pose``.

.. code-block:: console

  average rate: 59.354
    min: 0.005s max: 0.027s std dev: 0.00284s window: 58

Recuerda que configuraste la tasa de ``turtle1/cmd_vel`` para publicar a 1 Hz constante usando ``ros2 topic pub --rate 1``.
Si ejecutas el comando anterior con ``turtle1/cmd_vel`` en lugar de ``turtle1/pose``, verás un promedio que refleja esa tasa.

.. 9 rqt_plot
   ^^^^^^^^^^
   Can't do this section now because there's some significant UI issues with rqt_plot for ROS 2

9 Limpieza
^^^^^^^^^^

<<<<<<< HEAD
En este punto, tendrás muchos nodos en ejecución.
No olvides detenerlos introduciendo ``Ctrl+C`` en cada terminal.
=======
At this point you'll have a lot of nodes running.
Don't forget to stop them by entering ``Ctrl+C`` in each terminal.
>>>>>>> og

Resumen
-------

Los nodos publican información sobre topics, lo que permite que cualquier número de otros nodos se suscriban y accedan a esa información.
En este tutorial, examinaste las conexiones entre varios nodos sobre topics utilizando rqt_graph y herramientas de línea de comandos.
Ahora deberías tener una buena idea de cómo se mueven los datos en un sistema ROS 2.

Pasos siguientes
----------------

<<<<<<< HEAD
A continuación, aprenderás sobre otro tipo de comunicación en el grafo ROS con el tutorial :doc:`../Understanding-ROS2-Services/Understanding-ROS2-Services`
=======
Next you'll learn about another communication type in the ROS graph with the tutorial :doc:`../Understanding-ROS2-Services/Understanding-ROS2-Services`.
>>>>>>> og
