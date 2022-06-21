*****
Zappy
*****

Welcome to our Zappy documentation!
====================================

**Zappy** is the final project made in our second year in Epitech.
The goal of this project is to create a network game.
Several teams confront on a tiles map containing resources.
The winning team is the one with 6 players who reached maximum elevation.
The following documentation describe all the details and constraints.

Thus there is three parts to this project:

- **The server:** the project core that manages the entire game in a network.
- **The graphical interface:** interprets the commands received by the server and displays a result on a 3d map.
- **The artificial intelligence:** takes posession of the players to make them level up in an optimized way.

Schema
======
.. image:: assets/schema.png

Represents the interaction between SERVER/IA and SERVER/GUI
   
We suggest you to read the pages dedicated to each part: 
:ref:`Core:Core`, :ref:`Games:Games`, :ref:`Displays:Displays`, :ref:`Events:Events` & :ref:`Components:Components`

.. warning::

   Don't underestimate the difficulty of the project only by seeing this page.

Contents
========
.. toctree::
   Commands
   Teams
   Time
   Object
   Reproduction
   Inventory
   Broadcast
   Ejection