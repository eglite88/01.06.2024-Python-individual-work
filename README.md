# 01.06.2024-Python-individual-work


"""
Develop a simple prototype for an online shop
1. Define classes Client, Items, Transaction
2. Write the logic so that each client can purchase one of several items in a single transaction
3. Make a printout of data with nested loops
4. The program should print out:
- all clients
- all transactions of a client
- all items purchased in each transaction of the client
"""

import datetime

welcome_string = "Welcome to online shop 'Buy all what you need & dont need!' "
print(welcome_string)

class Client:
    number_of_clients = 0

    def __init__(self, name): 
        self.name = name
        self.items = [] 
        self.transactions = []
        Client.number_of_clients += 1

    def add_items(self, item): 
      self.items.append(item)

    def make_payment(self, item, amount, note):
        transaction = Transaction(item.currency, amount, note)
        self.transactions.append(transaction)
        item.transactions.append(transaction)


class Items:
    def __init__(self, name, currency, price = 0.0):
      self.name = name
      self.currency  = currency 
      self.price = price
      self.transactions = []
   

class Transaction:
    def __init__(self, currency, amount, note):
      self.currency = currency 
      self.amount = amount
      self.note = note 
      self.time_stamp = datetime.datetime.now() 


clients = []
clients.append(Client('Līga'))  
clients.append(Client('Uga'))   
clients.append(Client('Jānis'))  
clients.append(Client('Leo'))   

#Items 
clients[0].add_items(Items('Shoes', 'EUR', 28.50)) 
clients[0].add_items(Items('Supplements', 'EUR', 32.10)) 
clients[1].add_items(Items('Headphones', 'EUR', 120.99)) 
clients[1].add_items(Items('Powerbank', 'EUR', 83.65)) 
clients[1].add_items(Items('Charger', 'EUR', 17.30)) 
clients[2].add_items(Items('Candles', 'EUR', 17.20)) 
clients[3].add_items(Items('Toys', 'EUR', 9.99)) 
clients[3].add_items(Items('Sweets', 'EUR', 11.50)) 


#clients make payment
clients[0].make_payment(clients[0].items[0], 28.50, 'Shoes')
clients[0].make_payment(clients[0].items[1], 32.10, 'Supplements')
clients[1].make_payment(clients[1].items[0], 120.99, 'Headphones')
clients[1].make_payment(clients[1].items[1], 83.65, 'Powerbank')
clients[1].make_payment(clients[1].items[2], 17.30, 'Charger')
clients[2].make_payment(clients[2].items[0], 17.20, 'Candles')
clients[3].make_payment(clients[3].items[0], 9.99, 'Toys')
clients[3].make_payment(clients[3].items[1], 11.50, 'Sweets')

print(f'In our store "Buy all what you need & dont need!" in total purchased {Client.number_of_clients} clients:')

for client in clients: 
  print(f'Client {client.name} bought following items:')
  for item in client.items:
    print(f'    {item.name} ({item.currency}) {item.price}')
    for transaction in item.transactions:
      print(f'    {transaction.time_stamp} {transaction.currency} {transaction.amount}')
