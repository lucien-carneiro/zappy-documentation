**************
Part 1: Server
**************

Description
===========
Hello World

Communication
=============
In this part we will see in more details the communication protocol
and the management of the commands received by the server.

Connection
**********
As noticed on the diagram on the home page, the server communicates with the AI and the GUI:

- One function takes care of the GUI connection: *gui_command_connection*
- Another one takes care of the AI connection which takes possession of the players: *player_command_connection*.

.. code:: C

    void gui_command_connection(char **args, client_t *client)
    {
        for (size_t i = 0; GUI_COMMANDS[i].cmd; i++) {
            if (strcmp(GUI_COMMANDS[i].cmd, args[0]) == 0) {
                enqueue_command(client->player, args, &GUI_COMMANDS[i]);
                break;
            }
        }
    }

.. code:: C

    void player_command_connection(char **args, client_t *client)
    {
        for (size_t i = 0; PLAYER_COMMANDS[i].cmd; i++) {
            if (strcmp(PLAYER_COMMANDS[i].cmd, args[0]) == 0) {
                enqueue_command(client->player, args, &PLAYER_COMMANDS[i]);
                break;
            }
        }
    }

Commands Queue
**************
In order to receive a large number of commands and to be able to process them all,
we have set up a FIFO (First In First Out) type queue system:

.. code:: C

    void enqueue_command(player_t *player, char **args, command_t *command)
    {
        int i = 0;
        int j = 0;
        int nb_args = count_args(args);

        for (i = 0; player->command[i]; i++);
        if (i == MAX_COMMAND)
            return;
        player->command[i] = command;
        player->command[i]->args = malloc(sizeof(char *) * (nb_args + 1));
        if (player->command[i]->args == NULL)
            show_error("Malloc fail.");
        for (j = 0; args[j]; j++) {
            player->command[i]->args[j] = strdup(args[j]);
        }
        player->command[i]->args[j] = NULL;
    }


Here is the dequeue function which allows to exit the chain in order to execute the command entered:

.. code:: C

    void dequeue_command(player_t *player)
    {
        free_array(&(player->command[0]->args));
        for (int i = 0; player->command[i]; i++) {
            if (i == MAX_COMMAND) {
                player->command[i] = NULL;
                break;
            }
            player->command[i] = player->command[i + 1];
        }
    }

Player
======
We will explain the management of players in our server.

Inventory
*********
The player inventory is composed of two main parts:

- The foods that serve the survival of the player
- The ores which are used to make an incantation

.. code:: C

    typedef struct inventory_s {
        int food;
        int linemate;
        int deraumere;
        int sibur;
        int mendiane;
        int phiras;
        int thystame;
    } inventory_t;
