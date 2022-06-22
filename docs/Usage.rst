Usage
=====

To use Zappy Server:
.. code-block:: console

    ∼/B-YEP-410> ./zappy_server –help
    USAGE: ./zappy_server -p port -x width -y height -n name1 name2 ... -c clientsNb -f freq
        port        is the port number
        width       is the width of the world
        height      is the height of the world
        nameX       is the name of the team X
        clientsNb   is the number of authorized clients per team
        freq        is the reciprocal of time unit for execution of actions

To use Zappy GUI:
.. code-block:: console

    ∼/B-YEP-410> ./zappy_gui –help
    USAGE: ./zappy_ai -p port -h machine
        port        is the port number
        machine     is the name of the machine; localhost by default

To use Zappy IA:
.. code-block:: console

    ∼/B-YEP-410> ./zappy_ai –help
    USAGE: ./zappy_ai -p port -n name -h machine
        port        is the port number
        name        is the name of the team
        machine     is the name of the machine; localhost by default
