***********
Part 2: GUI
***********

Description
===========
To have a better vision of the game, which is simple, clear and ergonomic,
we made a user interface with the Unity engine.
We will describe below how our GUI works.

Main menu
=========
First of all, a main menu will appear.
To launch the game you just have to enter the ip of the server and its corresponding port.
In this menu, it is also possible to set the keys and the sensitivity.

.. image:: assets/gui_menu.png

Attempt server information
==========================
Once the connection information is filled in, the game will wait for information from the server (map size, game time, teams and players, ...).
When all the information sent by the server are received by the game, it will start the game automatically.

.. image:: assets/gui_loading.png

The complete game
=================
In the game, you can see the different islands that represent the tiles of the map.
Each island contains food and minerals.
The players move between the islands to collect resources.
In real time, the information of the map are displayed, as well as the broadcast of the players that can be deciphered.
By clicking on the islands or players, we can see what they contain (resources, inventory, ...)

.. image:: assets/gui_game.png
