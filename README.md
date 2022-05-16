# textbasedgame
text-based game I built in python

def instructions(): #defined instructions
    print("Code King Game")
    print("Collect 6 items to win the game, or be beaten by the Code King.")
    print("Move commands: South, North, East, West")
    print("Add to Inventory: get 'item name'")
    print("Type 'Exit' to exit game")


def move(direction, room = 'Entryway'): #created function for movement through rooms
        print('Moved to', rooms[room][direction])
        return rooms[room][direction]


#a dictionary for the Code King Game
#the dictionary links a room to other rooms/items
rooms = {
        'Entryway': {'East' : 'Great room'},
        'Great room': {'West' : 'Entryway', 'South' : 'Bedroom', 'North' : 'Living room', 'East' : 'Kitchen', 'Item' : 'Laptop'},
        'Bedroom': {'North' : 'Great room', 'East' : 'Library', 'Item' : 'Extra Monitor'},
        'Living room': {'South' : 'Great room', 'East' : 'Den', 'Item' : 'Mechanical Keyboard'},
        'Den': {'West' : 'Living room', 'Item' : 'Code King' },
        'Bathroom': {'South' : 'Kitchen', 'Item' : 'Rubber Duck'},
        'Kitchen': {'West' : 'Great room', 'North' : 'Bathroom', 'Item' : 'Coffee'},
        'Library': {'West' : 'Bedroom', 'Item' : 'Pseudocode'}
        }
#set variables
#set current room/location
#created list
#called instructions

direction = ''
stop = 'go'
location = 'Entryway'
inventory = []
instructions()
while stop != 'Exit': #started game while loop
    print('*******************************************')
    possible_moves = rooms[location].keys() #set possible moves
    print('Possible moves:', *possible_moves) #output possible moves
    print('Inventory:', *inventory) #output inventory
    print('You are in the', location) #output current location
    if 'Item' in rooms[location]: #if item is in the room
        print('You see a ' + rooms[location]['Item']) #output you see the item
    if location == 'Den' and len(inventory) != 6:  #if you enter the den without all the items you lose
        print("The Code King has found you out.....YOU LOSE!")
        exit(0)
    if location == 'Den' and len(inventory) == 6: #if you have all the items you win
        print("Congratulations! You have defeated the Code King, now you are the KING!")
        exit(0)
    direction = input('Which way?').title()  #set input variable/get input/title input to work with code
    print('You entered:', direction)  #repeat input
    if direction == 'Exit': #if input is exit stop
        print('Thanks for playing!')
        break
    if direction == 'East' or direction == 'West' or direction == 'North' or direction == 'South':  # if input is possible go that way
        location = move(direction, location)  # called function, moved rooms
    elif 'Item' in rooms[location] and direction == str('Get ' + rooms[location]['Item']): #if item in room get item
        inventory.append(rooms[location]['Item'])  # if you dont have item put item in inventory and remove from dict
        rooms[location].pop('Item')
    else:
        print('Invalid direction! Please enter a valid direction.') #if input is invalid error message

