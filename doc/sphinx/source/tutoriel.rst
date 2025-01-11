#####################
Tutoriel DynamixelSDK
#####################

.. note::
   Ce tutoriel est basé sur le tutoriel officiel de ROBOTIS. Vous pouvez le consulter `ici <https://emanual.robotis.com/docs/en/software/dynamixel/dynamixel_sdk/overview/>`_.

********
PC Setup
********

Création d'un espace de travail pour télécharger et installer la librairie.

Download DynamixelSDK
=====================

.. code-block:: bash

   mkdir -p ~/robotics_ws/src
   cd ~/robotics_ws/src
   git clone -b $ROS_DISTRO-devel https://github.com/ROBOTIS-GIT/DynamixelSDK

Install DynamixelSDK
====================

Téléchagement et installation de la librairie.

.. code-block:: bash

   cd ~/robotics_ws && colcon build --symlink-install
   source /opt/ros/$ROS_DISTRO/setup.bash
   cd ~/robotics_ws
   . install/setup.bash

***
Run
***

Vérification de la connexion USB
================================

Vérifier la connexion USB de votre appareil.
Autoriser l'accès à l'utilisateur.
Lancer le noeud de lecture/écriture.

.. code-block:: bash

   ls -l /dev/tty*
   sudo usermod -aG dialout $USER
   ros2 run dynamixel_sdk_examples read_write_node

Ouvrir un autre terminal et lancer la commande suivante :

.. note::
   Remplacer ``/dev/ttyUSB0`` par le port USB de votre appareil.*
   
      .. code-block:: bash

         ros2 topic echo /dynamixel_workbench/torque_enable