.. redirect-from::

    Tutorials/Parameters/Understanding-ROS2-Parameters

.. _ROS2Params:

Comprender los Parámetros
=========================

**Objetivo:** Aprenda a obtener, configurar, guardar y recargar parámetros en ROS 2.

**Nivel del Tutorial:** Principiant

**Tiempo:** 5 minutos

.. contents:: Contenido
   :depth: 2
   :local:

Historial
---------

Un parámetro es un valor de configuración de un nodo.
Puedes pensar en los parámetros como configuraciones de nodo.
Un nodo puede almacenar parámetros como enteros, flotantes, booleanos, cadenas y listas.
En ROS 2, cada nodo mantiene sus propios parámetros.
Para obtener más información sobre los parámetros, puedes consultar :doc:`el documento de conceptos<../../../Concepts/About-ROS-2-Parameters>`.

Requisitos previos
------------------

Este tutorial utiliza el paquete :doc:`turtlesim <../Introducing-Turtlesim/Introducing-Turtlesim>`.

<<<<<<< HEAD
Como siempre, no olvides ejecutar `source` con el archivo de setup :doc:`en cada nueva terminal que abra<../Configuring-ROS2-Environment>`.
=======
As always, don't forget to source ROS 2 in :doc:`every new terminal you open <../Configuring-ROS2-Environment>`.
>>>>>>> og

Tareas
------

1 Configuración
^^^^^^^^^^^^^^^

Inicia los dos nodos de turtlesim, ``/turtlesim`` y ``/teleop_turtle``.

Abra una nueva terminal y ejecute:

.. code-block:: console

    ros2 run turtlesim turtlesim_node

Abre otra terminal y ejecuta:

.. code-block:: console

    ros2 run turtlesim turtle_teleop_key


2 ros2 param list
^^^^^^^^^^^^^^^^^

Para ver los parámetros que pertenecen a sus nodos, abre una nueva terminal e introduce el comando:

.. code-block:: console

    ros2 param list

<<<<<<< HEAD
Verás los espacios de nombres de los nodos, ``/teleop_turtle`` y ``/turtlesim``, seguidos de los parámetros de cada nodo:
=======
You will see the node namespaces, ``/teleop_turtle`` and ``/turtlesim``, followed by each node's parameters:
>>>>>>> og

.. code-block:: console

  /teleop_turtle:
    qos_overrides./parameter_events.publisher.depth
    qos_overrides./parameter_events.publisher.durability
    qos_overrides./parameter_events.publisher.history
    qos_overrides./parameter_events.publisher.reliability
    scale_angular
    scale_linear
    use_sim_time
  /turtlesim:
    background_b
    background_g
    background_r
    qos_overrides./parameter_events.publisher.depth
    qos_overrides./parameter_events.publisher.durability
    qos_overrides./parameter_events.publisher.history
    qos_overrides./parameter_events.publisher.reliability
    use_sim_time

<<<<<<< HEAD
Cada nodo tiene el parámetro ``use_sim_time``; no es exclusivo de turtlesim.
=======
Every node has the parameter ``use_sim_time``; it's not unique to turtlesim.
>>>>>>> og

Según sus nombres, parece que los parámetros de ``/turtlesim`` determinan el color de fondo de la ventana de turtlesim usando valores de color RGB.

Para determinar el tipo de un parámetro, puede usar ``ros2 param get``.


3 ros2 param get
^^^^^^^^^^^^^^^^

Para mostrar el tipo y el valor actual de un parámetro, use el comando:

.. code-block:: console

    ros2 param get <node_name> <parameter_name>

<<<<<<< HEAD
Por ejemplo, para ver el valor actual del parámetro ``background_g`` de ``/turtlesim``, ejecuta:
=======
Let's find out the current value of ``/turtlesim``'s parameter ``background_g``:
>>>>>>> og

.. code-block:: console

    ros2 param get /turtlesim background_g

Lo que devolverá el valor:

.. code-block:: console

    Integer value is: 86

Now you know ``background_g`` holds an integer value.

Ahora sabes que ``background_g`` tiene un valor entero.

Si ejecutas el mismo comando en ``background_r`` y ``background_b``, obtendrás los valores 69 y 255, respectivamente.

4 ros2 param set
^^^^^^^^^^^^^^^^

Para cambiar el valor de un parámetro en tiempo de ejecución, usa el comando:

.. code-block:: console

    ros2 param set <node_name> <parameter_name> <value>

<<<<<<< HEAD
Cambiemos el color de fondo de ``/turtlesim``:
=======
Let's change ``/turtlesim``'s background color:
>>>>>>> og

.. code-block:: console

    ros2 param set /turtlesim background_r 150

La terminal debería devolver el mensaje:

.. code-block:: console

  Set parameter successful

Y el fondo de la ventana de turtlesim debería cambiar de color:

.. image:: images/set.png

Establecer parámetros con el comando ``set`` solo los cambiará en su sesión actual, no de forma permanente.
Sin embargo, puedes guardar tu configuración y volver a cargarla la próxima vez que inicie un nodo.

5 ros2 param dump
^^^^^^^^^^^^^^^^^

<<<<<<< HEAD
Puedes ver todos los parámetros y sus valores actuales de un nodo usando el comando:
=======
You can view all of a node's current parameter values by using the command:
>>>>>>> og

.. code-block:: console

  ros2 param dump <node_name>

<<<<<<< HEAD
El comando se imprime en la salida estándar (stdout) de forma predeterminada, pero también puede redirigir los valores de los parámetros a un archivo para guardarlos más adelante.
Para guardar la configuración actual de los parámetros de ``/turtlesim`` en el archivo ``turtlesim.yaml``, introduce el comando:
=======
The command prints to the standard output (stdout) by default but you can also redirect the parameter values into a file to save them for later.
To save your current configuration of ``/turtlesim``'s parameters into the file ``turtlesim.yaml``, enter the command:
>>>>>>> og

.. code-block:: console

  ros2 param dump /turtlesim > turtlesim.yaml

<<<<<<< HEAD
Encontrarás un nuevo archivo en el directorio de trabajo en el que se está ejecutando tu terminal.
Si abres este archivo, verá el siguiente contenido:
=======
You will find a new file in the current working directory your shell is running in.
If you open this file, you'll see the following content:
>>>>>>> og

.. code-block:: YAML

  /turtlesim:
    ros__parameters:
      background_b: 255
      background_g: 86
      background_r: 150
      qos_overrides:
        /parameter_events:
          publisher:
            depth: 1000
            durability: volatile
            history: keep_last
            reliability: reliable
      use_sim_time: false

Guardar los parámetros resulta útil si deseas volver a cargar el nodo con los mismos parámetros en el futuro.

6 ros2 param load
^^^^^^^^^^^^^^^^^

Puedes cargar parámetros desde un archivo a un nodo actualmente en ejecución usando el comando:

.. code-block:: console

  ros2 param load <node_name> <parameter_file>

<<<<<<< HEAD
Para cargar el archivo ``turtlesim.yaml`` generado con ``ros2 param dump`` en los parámetros del nodo ``/turtlesim``, introduce el comando:
=======
To load the ``turtlesim.yaml`` file generated with ``ros2 param dump`` into ``/turtlesim`` node's parameters, enter the command:
>>>>>>> og

.. code-block:: console

  ros2 param load /turtlesim turtlesim.yaml

La terminal devolverá el mensaje:

.. code-block:: console

  Set parameter background_b successful
  Set parameter background_g successful
  Set parameter background_r successful
  Set parameter qos_overrides./parameter_events.publisher.depth failed: parameter 'qos_overrides./parameter_events.publisher.depth' cannot be set because it is read-only
  Set parameter qos_overrides./parameter_events.publisher.durability failed: parameter 'qos_overrides./parameter_events.publisher.durability' cannot be set because it is read-only
  Set parameter qos_overrides./parameter_events.publisher.history failed: parameter 'qos_overrides./parameter_events.publisher.history' cannot be set because it is read-only
  Set parameter qos_overrides./parameter_events.publisher.reliability failed: parameter 'qos_overrides./parameter_events.publisher.reliability' cannot be set because it is read-only
  Set parameter use_sim_time successful

.. note::

  Los parámetros de solo lectura solo se pueden modificar al inicio y no después, por eso hay algunas advertencias para los parámetros 'qos_overrides'.

7 Cargar archivo de parámetros al iniciar el nodo
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Para iniciar el mismo nodo usando los valores de parámetros guardados, ejecuta:

.. code-block:: console

  ros2 run <package_name> <executable_name> --ros-args --params-file <file_name>

<<<<<<< HEAD
Stop your running turtlesim node so you can try reloading it with your saved parameters, using:
Este es el mismo comando que utilizas para iniciar turtlesim, con las banderas añadidas ``--ros-args`` y ``--params-file``, seguidas del archivo que desea cargar.

Intentá detener el nodo turtlesim en ejecución, para volver a cargarlo con sus parámetros guardados usando:
=======
This is the same command you always use to start turtlesim, with the added flags ``--ros-args`` and ``--params-file``, followed by the file you want to load.

Stop your running turtlesim node, and try reloading it with your saved parameters, using:
>>>>>>> og

.. code-block:: console

  ros2 run turtlesim turtlesim_node --ros-args --params-file turtlesim.yaml

La ventana de turtlesim debería aparecer como de costumbre, pero con el fondo morado que configuraste anteriormente.

.. note::

<<<<<<< HEAD
  En este caso, los parámetros se modifican al inicio, por lo que los parámetros de solo lectura especificados también tendrán efecto.
=======
  When a parameter file is used at node startup, all parameters, including the read-only ones, will be updated.
>>>>>>> og

Resumen
-------

Los nodos tienen parámetros para definir sus valores de configuración predeterminados.
Puedes obtener y establecer valores de parámetros desde la línea de comandos.
También puedes guardar la configuración de los parámetros en un archivo para volver a cargarlos en una sesión futura.

Pasos siguientes
----------------

Volviendo a los métodos de comunicación de ROS 2, en el próximo tutorial aprenderás sobre :doc:`acciones <../Understanding-ROS2-Actions/Understanding-ROS2-Actions>`.
