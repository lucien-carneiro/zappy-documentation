********
Commands
********

Description
===========
In order to better define the communication protocol,
we have made a summary table of the different commands used for the server transmission and the user interface reception.
A small description of each command is listed in the table and all parameters are defined in the index.

Index
=====
- **X** width or horizontal position
- **Y** height or vertical position
- **q0** resource 0 (food) quantity
- **q1** resource 1 (linemate) quantity
- **q2** resource 2 (deraumere) quantity
- **q3** resource 3 (sibur) quantity
- **q4** resource 4 (mendiane) quantity
- **q5** resource 5 (phiras) quantity
- **q6** resource 6 (thystame) quantity

- **n** player number
- **O** orientation: 1(N), 2(E), 3(S), 4(W)
- **L** player or incantation level
- **e** egg number
- **T** time unit
- **N** name of the team
- **R** incantation result
- **M** message
- **I** resource number

Commands
========
+---------------------------------------+--------------+------------------------------------------------+
|           SERVER MESSAGES             | GUI COMMANDS |                  DESCRIPTION                   |
+=======================================+==============+================================================+
|msz X Y                                |msz X Y       |map size                                        |
+---------------------------------------+--------------+------------------------------------------------+
|bct X Y q0 q1 q2 q3 q4 q5 q6           |bct X Y       |content of a tile                               |
+---------------------------------------+--------------+------------------------------------------------+
|bct X Y q0 q1 q2 q3 q4 q5 q6\n * nb    |mct           |content of the map (all the tiles)              |
+---------------------------------------+--------------+------------------------------------------------+
|tna N\n * nbr_teams                    |tna           |name of all the teams                           |
+---------------------------------------+--------------+------------------------------------------------+
|pnw n X Y O L N                        |              |creation of a new player                        |
+---------------------------------------+--------------+------------------------------------------------+
|pns n R                                |              |player state ( 1 alive, 0 not used )            |
+---------------------------------------+--------------+------------------------------------------------+
|ppo n X Y O                            |ppo #n        |player???s position                               |
+---------------------------------------+--------------+------------------------------------------------+
|plv n L                                |plv #n        |player???s level                                  |
+---------------------------------------+--------------+------------------------------------------------+
|pin n q0 q1 q2 q3 q4 q5 q6             |pin #n        |player???s inventory                              |
+---------------------------------------+--------------+------------------------------------------------+
|pex n                                  |              |explusion                                       |
+---------------------------------------+--------------+------------------------------------------------+
|pbc n M                                |              |broadcast                                       |
+---------------------------------------+--------------+------------------------------------------------+
|pic X Y L n n ???                        |              |start of an incantation (by the first player)   |
+---------------------------------------+--------------+------------------------------------------------+
|pie X Y R                              |              |end of an incantation                           |
+---------------------------------------+--------------+------------------------------------------------+
|pdr n i                                |              |resource dropping                               |
+---------------------------------------+--------------+------------------------------------------------+
|pgt n i                                |              |resource collecting                             |
+---------------------------------------+--------------+------------------------------------------------+
|pdi n                                  |              |death of a player                               |
+---------------------------------------+--------------+------------------------------------------------+
|enw n e X Y                            |              |an egg was laid by a player                     |
+---------------------------------------+--------------+------------------------------------------------+
|eht e                                  |              |egg hatching                                    |
+---------------------------------------+--------------+------------------------------------------------+
|sgt T                                  |sgt           |time unit request                               |
+---------------------------------------+--------------+------------------------------------------------+
|seg N                                  |              |end of game                                     |
+---------------------------------------+--------------+------------------------------------------------+
|suc                                    |              |unknown command                                 |
+---------------------------------------+--------------+------------------------------------------------+
|sbp                                    |              |command parameter                               |
+---------------------------------------+--------------+------------------------------------------------+
|look                                   |              |look animation                                  |
+---------------------------------------+--------------+------------------------------------------------+
|pgte n R                               |              |take ressource end 1 or 0                       |
+---------------------------------------+--------------+------------------------------------------------+
|pexed n X Y                            |              |ejected to this coords                          |
+---------------------------------------+--------------+------------------------------------------------+
|pnw and pin                            |pls           |get all players at start                        |
+---------------------------------------+--------------+------------------------------------------------+