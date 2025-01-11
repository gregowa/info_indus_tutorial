#########
Prérequis
#########

**********************
Installation de VSCode
**********************

****************************************************
Installation de ROS 2 Humble pour Ubuntu Linux 22.04
****************************************************

Installer ROS 2 Humble pour Ubuntu Linux 22.04 avant de commencer le tutoriel.

Suivre l'installation jusqu'au point **Install additional DDS implementations (optional)**.

`Lien vers l'installation <https://docs.ros.org/en/humble/Installation/Alternatives/Ubuntu-Development-Setup.html>`_

********************************************
Création d'un compte Github et d'une clé SSH
********************************************

Suivre le tutoriel sur ce lien pour créer un compte Github et créer une clé SSH :

`Tutoriel <https://yguel.github.io/informatique_industrielle_avec_ROS2/c01_create_and_publish_doc/p01s05_www_doc.html#creer-un-depot-sur-github>`_

.. note::
   Si on vous demande de vous connecter avec un nom d'utilisateur et un mot de passe, cela signifie que vous utilisez l'URL HTTPS pour cloner le dépôt. 
   Pour éviter cela, vous pouvez utiliser une clé SSH. Voici les étapes à suivre :

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