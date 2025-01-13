#####################
Tutoriel DynamixelSDK
#####################

.. note::
   Ce tutoriel est basé sur le tutoriel YouTube de ROBOTIS OpenSourceTeam. Vous pouvez le consulter `ici <https://www.youtube.com/watch?v=E8XPqDjof4U/>`_.

**********************
Installer DynamixelSDK
**********************

Commencer par créer un dossier de travail et cloner le dépôt de DynamixelSDK en remplaçant ``$ROS_DISTRO`` par votre distribution ROS (ex: foxy, humble, etc.).

.. code-block:: bash

   mkdir -p ~/robotics_ws/src
   cd ~/robotics_ws/src
   git clone -b $ROS_DISTRO-devel https://github.com/ROBOTIS-GIT/DynamixelSDK

On construit les paquets ROS 2 en utilisant la commande ``colcon build`` dans notre espace de travail.

.. code-block:: bash

   cd ~/robotics_ws && colcon build --symlink-install
   source /opt/ros/$ROS_DISTRO/setup.bash
   cd ~/robotics_ws
   . install/setup.bash

*******************
Lancer DynamixelSDK
*******************

Vérification de la connexion USB
================================

Vérifier la connexion USB de votre appareil.
Autoriser l'accès à l'utilisateur.
Lancer le noeud de lecture/écriture.

.. code-block:: bash

   ls -l /dev/tty*
   sudo usermod -aG dialout $USER
   ros2 run dynamixel_sdk_examples read_write_node

Ouvrir un autre terminal et lancer la commande suivante afin de publier un message de position sur le topic /set_position. On appelle le moteur en utilisant l'ID 1 et en lui envoyant une position de 512.

.. code-block:: bash

   ros2 topic pub -l /set_position dynamixel_sdk_custom_interfaces/SetPosition "{id: 1, position: 1000}"

.. note::

   Pour vérifier l'état du couple moteur, il est recommandé de lancer la commande à l'aide de la commande suivante :

.. code-block:: bash

   ros2 topic echo /dynamixel_workbench/dynamixel_state
   ros2 topic echo /dynamixel_workbench/torque_enable

On appelle le serive /get_position de lecture de position en utilisant l'ID 1.

.. code-block:: bash

   ros2 service call /get_position dynamixel_sdk_custom_interfaces/srv/GetPosition "{id: 1}"

On peut publier un message /set_position en utilisant l'ID 1 et en lui envoyant une position de 0 par exemple.

.. code-block:: bash

   ros2 topic pub -l /set_position dynamixel_sdk_custom_interfaces/SetPosition "{id: 1, position: 0}"