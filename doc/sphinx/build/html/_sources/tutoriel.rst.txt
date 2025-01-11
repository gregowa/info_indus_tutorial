#####################
Tutoriel DynamixelSDK
#####################

*****
Setup
*****

.. code-block:: bash

   mkdir -p ~/robotics_ws/src
   cd ~/robotics_ws/src
   git clone -b $ROS_DISTRO-devel https://github.com/ROBOTIS-GIT/DynamixelSDK

ne pas oublier de prendre la bonne version
humble
et depth

.. note::
   Si on vous demande de vous connecter avec un nom d'utilisateur et un mot de passe, cela signifie que vous utilisez l'URL HTTPS pour cloner le dépôt. 
   Pour éviter cela, vous pouvez utiliser une clé SSH suivre le tutoriel des prérequis.

******
Build
******

.. code-block:: bash

   cd ~/robotics_ws && colcon build --symlink-install