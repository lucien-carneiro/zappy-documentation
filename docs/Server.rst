**************
Part 2: Server
**************

Description
===========


Commands Queue
==============
In order to receive a large number of commands and to be able to process them all,
we have set up a FIFO (First In First Out) type queue system.

.. code-blocks:: C

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
.. code-blocks:: C

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
