############
Introduction
############

Le pantographe est un dispositif mécanique utilisé pour copier, agrandir ou réduire des dessins. Il est composé de plusieurs bras articulés qui permettent de reproduire fidèlement les mouvements d'un stylet sur une surface de travail. Dans ce projet, nous allons utiliser un pantographe pour dessiner des formes géométriques simples sur une feuille de papier. Pour cela, nous allons contrôler les servomoteurs Dynamixel AX12A à l'aide d'une Raspberry Pi 5 et d'un U2D2 Power Hub Board.

Maquette
========

Pour dessiner des formes géométriques simples, nous allons utiliser un pantographe ci-dessous :

.. figure:: ressources/img/pantographe.png
   :align: center
   :width: 600px
   :alt: Pantographe pour dessiner des formes géométriques simples

   Pantographe pour dessiner des formes géométriques simples

Configuration
=============

Pour contrôler les servomoteurs Dynamixel AX12A du pantographe, voici comment brancher les différents composants :

.. figure:: ressources/img/setup.jpg
   :align: center
   :width: 600px
   :alt: Configuration pour le contrôle des servomoteurs Dynamixel AX12A avec une Raspberry Pi 5 et un U2D2 Power Hub

   Branchement des servomoteurs Dynamixel AX12A avec une Raspberry Pi 5 et un U2D2 Power Hub