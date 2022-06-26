**********
Part 3: IA
**********

Description
===========
Each player of the game is by default inactive, to animate a player the artificial intelligence must take possession of it.
To do this, it must communicate with the server and send it precise instructions.
**Its objective:** reach level 8 as soon as possible!

Initialisation
==============

Client interface
****************
Here is Client class constructor:

.. code:: python

    self.team = team_name
    self.hostname = hostname
    self.port = port
    self.client_num = 0
    self.data = Data(0, 0)
    self.socket = None
    self.selectors = selectors.DefaultSelector()
    self.just_log = 0
    self.logged = 0
    self.ia = IA(self.team)

Server Connection
*****************
Initialise a socket which connects to the server.
We initialize the selectors to and be sure to receive the Welcome message.

.. code:: python

    def connect_to_server(self):
        self.socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        self.socket.setblocking(False)
        self.socket.connect_ex((self.hostname, safe_cast(self.port, int)))
        events = selectors.EVENT_READ | selectors.EVENT_WRITE
        self.selectors.register(self.socket, events)

Algorithm
=========
The AI engine is based on a shared inventory
algorithm that allows all players in the team to know the resources needed for the incantation.
Below is the main source code of the algorithm:

.. code:: python

    def algorithm(self):
        if self.step == -1:
            self.data_to_write = "Connect_nbr\n"
            self.step += 1
        elif self.step == 0:
            if self.commands_list:
                self.data_to_write = self.commands_list[0]
                self.commands_list = self.commands_list[1:]
            else:
                self.data_to_write = "Inventory\n"
                self.step += 1
        elif self.step == 1:
            if self.new_object:
                if not self.check_incantation():
                    message = bytes(self.sxor(self.team, ("inventory" + str(self.client_num) + ";" + str(self.level) + ";" + str(json.dumps(self.inventory)))), "utf-8").hex()
                    self.data_to_write = "Broadcast " + message + "\n"
                else:
                    message = bytes(self.sxor(self.team, (str(self.client_num) + ";incantation;" + str(self.level))), "utf-8").hex()
                    self.data_to_write = "Broadcast " + message + "\n"
                    self.master_incantation = 1
                    self.step = 4
                    self.incantation = 1
                    self.new_object = False
                    return
                self.new_object = False
            else:
                self.step += 1
                self.algorithm()
                return
            self.step += 1
        elif self.step == 2:
            if "food" in self.inventory and self.inventory["food"] < 15:
                self.data_to_write = "Look\n"
            else:
                self.step += 1
                self.algorithm()
                return
            self.step += 1
        elif self.step == 3:
            if "food" in self.inventory and self.inventory["food"] < 15:
                self.commands_list = self.parse_look(self.look, "food")
                self.step = 0
            else:
                self.to_search = self.search_good_ressources()
                self.commands_list = self.parse_look(self.look, self.to_search)
                self.step = 0
        elif self.step == 4:
            if self.incantation == 0:
                data = bytes(self.sxor(self.team, str(self.client_num) + " on my way"), "utf-8").hex()
                self.data_to_write = "Broadcast " + data + "\n"
                self.incantation = 1
                return
            if self.master_incantation >= 6:
                self.step += 1
                return
            if self.master_incantation >= 1:
                pass
            elif self.commands_list and not self.ready_for_incantation:
                self.data_to_write = self.commands_list[0]
                self.commands_list = self.commands_list[1:]
                self.clear_broadcast = 1
                if not self.commands_list:
                    self.clear_read = 1
            elif self.ready_for_incantation and "Broadcast" in self.data_to_write:
                self.step += 1
            else:
                self.data_to_write = ""
        elif self.step == 5:
            self.clear_broadcast = 0
            self.data_to_write = "Look\n"
            self.step += 1
        elif self.step == 6:
            if self.master_incantation >= 6:
                self.start_incantation()
            if self.step != 7:
                self.drop_object_incantation()
                if self.commands_list:
                    self.data_to_write = self.commands_list[0]
                    self.commands_list = self.commands_list[1:]
                else:
                    self.data_to_write = "Inventory\n"
        elif self.step == 7:
            if self.master_incantation < 6:
                self.data_to_write = ""
                return
            if self.commands_list:
                    print(self.level, " ", self.look)
                    self.data_to_write = self.commands_list[0]
                    self.commands_list = self.commands_list[1:]
            else:
                self.commands_list = ["Inventory\n"]
                self.commands_list = ["Look\n"]
        elif self.step == 8:
            self.data_to_write = ""
