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

.. note::
   Si on vous demande de vous connecter avec un nom d'utilisateur et un mot de passe, cela signifie que vous utilisez l'URL HTTPS pour cloner le dépôt. Pour éviter cela, vous pouvez utiliser une clé SSH. Voici les étapes à suivre :

   1. Générer une clé SSH (si vous n'en avez pas déjà une) :

      .. code-block:: bash

         ssh-keygen -t rsa -C "your_email@example.com" -f .ssh/id_rsa

   2. Ajouter la clé SSH à votre compte GitHub :

      - Copiez le contenu de votre clé publique :

         .. code-block:: bash
            
            cat ~/.ssh/id_rsa.pub

      - Ajoutez cette clé à votre compte GitHub sous **Settings > SSH and GPG keys**.

   3. Mettre à jour la commande de clonage pour utiliser l'URL SSH :

      .. code-block:: bash
         
         git clone -b $ROS_DISTRO-devel git@github.com:ROBOTIS-GIT/DynamixelSDK.git

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

Vérifier la connexion USB de votre appareil et autoriser l'accès à l'utilisateur ``$USER`` puis lancer le noeud de lecture/écriture.

.. code-block:: bash

   ls -l /dev/tty*
   sudo usermod -aG dialout $USER
   ros2 run dynamixel_sdk_examples read_write_node

Contrôle du moteur
==================

Ouvrir un autre terminal et lancer la commande suivante afin de publier un message de position sur le topic ``/set_position``. On appelle le moteur en utilisant l'ID 1 et en lui envoyant une position de 512.

.. code-block:: bash

   ros2 topic pub -l /set_position dynamixel_sdk_custom_interfaces/SetPosition "{id: 1, position: 1000}"

.. note::

   Pour vérifier l'état du couple moteur, il est recommandé de lancer la commande à l'aide de la commande suivante :

   .. code-block:: bash

      ros2 topic echo /dynamixel_workbench/dynamixel_state
      ros2 topic echo /dynamixel_workbench/torque_enable

On appelle le serive ``/get_position`` de lecture de position en utilisant l'ID 1.

.. code-block:: bash

   ros2 service call /get_position dynamixel_sdk_custom_interfaces/srv/GetPosition "{id: 1}"

On peut publier un message ``/set_position`` en utilisant l'ID 1 et en lui envoyant une position de 0 par exemple.

.. code-block:: bash

   ros2 topic pub -l /set_position dynamixel_sdk_custom_interfaces/SetPosition "{id: 1, position: 0}"

*******************
Example de code C++
*******************

Code complet
============

Il est maintenant le temps de réaliser un exemple de code C++ pour lire et écrire des données sur un moteur Dynamixel AX12A. Vous pouvez consulter le code complet ci-dessous. Les parties importantes du code sont surlignées et expliquées dans la partie suivante.

.. raw:: html

   <details>
   <summary>Afficher le code complet :</summary>

.. literalinclude:: ressources/code/read_write_node.cpp
   :language: cpp
   :caption: Fichier cpp read_write_node.cpp
   :linenos:
   :emphasize-lines: 15-28, 74-105, 107-133, 174-175

.. raw:: html

   </details>

.. raw:: html

   <br><br>

Explication du code
===================

Cette partie décrit comment exécuter l'exemple, comment publier sur le topic ``/set_position`` et comment faire une requête de service pour lire la position du moteur.

.. literalinclude:: ressources/code/read_write_node.cpp
   :language: cpp
   :caption: Lignes 15 à 28 du fichier read_write_node.cpp
   :lineno-start: 15
   :lines: 15-28

Cette partie du code définit ``set_position_subscriber_`` pour souscrire au topic ``/set_position`` et appeler la fonction ``setPositionCallback`` à chaque fois qu'un message est publié sur ce topic.

.. literalinclude:: ressources/code/read_write_node.cpp
   :language: cpp
   :caption: Lignes 74 à 105 du fichier read_write_node.cpp
   :lineno-start: 74
   :lines: 74-105

Cette partie du code définit le service ``get_position_service_`` pour lire la position du moteur en utilisant l'ID fourni dans la requête de service.

.. literalinclude:: ressources/code/read_write_node.cpp
   :language: cpp
   :caption: Lignes 107 à 133 du fichier read_write_node.cpp
   :lineno-start: 107
   :lines: 107-133

Dans le main, on initialise ``portHandler_`` et ``packetHandler_`` pour communiquer avec le moteur.

.. literalinclude:: ressources/code/read_write_node.cpp
   :language: cpp
   :caption: Lignes 174 à 175 du fichier read_write_node.cpp
   :lineno-start: 174
   :lines: 174-175